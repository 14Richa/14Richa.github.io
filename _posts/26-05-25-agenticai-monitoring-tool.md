---
layout: post
title: "Building a Network Ops AI Agent with Google ADK in One Day"
author: "Richa"
---

It started with a calendar invite: "Google ADK Hackathon — All Night."

The Google team was joining live from our Denver office - big leaders, on a call, watching. From Hyderabad, that meant one thing: we were doing this through the night.

By 9 PM our office was a different place. The usual hum of meetings and standups was gone. It was just our team of four, laptops open, empty coffee cups slowly accumulating, and a Google Meet window in the corner showing Denver. That particular mix of exhaustion and adrenaline that only a night hackathon produces - you either know it or you don't.

The stakes felt real. This wasn't an internal demo for a small team. Senior leaders were watching from across the world, and we had until morning to show them something worth staying up for.

Our team huddled up and asked the question every hackathon team asks: what problem do we actually care about solving?
We didn't have to think long.

Anyone who's worked in an office with network infrastructure knows the pain. Monitoring tools like ManageEngine, Statseeker, and SD-WAN vManage each generate their own stream of alerts — high latency here, packet loss there, an interface going down at 2 AM. And the tricky part? A single real incident can trigger alerts across all three tools at once, leaving an engineer jumping between dashboards to piece together what's actually happening.
That triage process? It's repetitive, mentally taxing, and it happens dozens of times a day.

We thought: what if an AI agent could do the first pass?

## What We Built

By the end of the hackathon, we had a working agent — let's call it **NetSense** — that could:

- **Ingest raw alerts** from ManageEngine in real time
- **Understand the context** behind each alert (what device, what metric, what threshold was crossed)
- **Query 6 months of historical alert data** stored in BigQuery to spot recurring patterns
- **Correlate related alerts** to identify whether something is a one-off or a known recurring issue
- **Generate a plain-English summary** of what's happening and how urgent it is
- **Suggest solutions** based on what actually worked the last time this happened
That last point is what made it genuinely useful. Instead of an engineer staring at 47 alerts and deciding where to start, NetSense would hand them a prioritized briefing — *and* tell them what resolved the same issue six months ago.

Think of it as a first-responder that never sleeps, never gets alert fatigue, and has a perfect memory of everything that's ever gone wrong on your network.

### Why BigQuery?

We loaded **6 months of historical ManageEngine alert data** into BigQuery and gave the agent a tool to query it. This was a game-changer.

Without history, the agent could only describe what's happening *right now*. With history, it could answer questions like:

- *"Has this device had latency issues before?"*
- *"Is packet loss on this switch a recurring Monday morning pattern?"*
- *"What did the team do last time this exact alert fired?"*
This turned NetSense from a smart summarizer into something closer to an **institutional memory** — one that doesn't leave when engineers switch teams or change jobs.

## Enter Google ADK

Google's **Agent Development Kit (ADK)** is a framework for building multi-step AI agents powered by Gemini. What makes it interesting is that it's not just a wrapper around an LLM — it gives you a structured way to define:

- **Tools** your agent can call (functions, APIs, data sources)
- **A reasoning loop** where the agent decides what to do next
- **Memory and context** so the agent can build up understanding across steps
For our use case, this was exactly what we needed. Analyzing network alerts isn't a single-prompt job. It requires the agent to look at an alert, fetch more context, compare it against history, and reason about what it all means together.

Here's a simplified version of how we set up a tool for the agent:

```python
from google.adk.agents import Agent
from google.adk.tools import FunctionTool
from google.cloud import bigquery

def get_alert_history(device_id: str, hours: int = 24) -> dict:
    """Fetch recent alerts for a specific network device."""
    # In production, this calls your ManageEngine API
    return {
        "device_id": device_id,
        "alerts": [
            {"time": "2026-05-24T08:12:00", "type": "high_latency", "value": "320ms"},
            {"time": "2026-05-24T09:45:00", "type": "packet_loss", "value": "4.2%"},
        ]
    }

def get_device_info(device_id: str) -> dict:
    """Get metadata about a network device."""
    return {
        "device_id": device_id,
        "name": "core-switch-floor3",
        "location": "Building A, Floor 3",
        "criticality": "high"
    }

def query_historical_alerts(device_id: str, alert_type: str) -> dict:
    """Query 6 months of historical alert data from BigQuery to find patterns and past resolutions."""
    client = bigquery.Client()
    query = f"""
        SELECT
            alert_type,
            occurred_at,
            resolution,
            resolved_by,
            time_to_resolve_mins
        FROM `your_project.network_ops.alerts_history`
        WHERE device_id = '{device_id}'
          AND alert_type = '{alert_type}'
          AND occurred_at >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 180 DAY)
        ORDER BY occurred_at DESC
        LIMIT 10
    """
    results = client.query(query).result()
    return {
        "historical_incidents": [dict(row) for row in results],
        "message": f"Found past incidents for {device_id} — includes resolution steps"
    }

# Register all three tools and create the agent
alert_tool = FunctionTool(get_alert_history)
device_tool = FunctionTool(get_device_info)
history_tool = FunctionTool(query_historical_alerts)

agent = Agent(
    model="gemini-2.0-flash",
    tools=[alert_tool, device_tool, history_tool],
    system_prompt="""You are a network operations analyst with access to
    real-time alerts and 6 months of historical incident data.
    When given an alert, investigate it using available tools, check if this
    is a recurring issue, identify the root cause, assess urgency, and suggest
    solutions based on what has worked in the past."""
)
```

What the agent then does — on its own — is decide *which* tools to call, in *what order*, based on what it learns along the way. You don't hardcode the logic. The agent reasons through it.

---

## The Moment It Clicked

About four hours into the hackathon, we fed the agent a batch of real-looking test alerts we'd mocked up — things like:

```
[ALERT] core-switch-floor3 | Latency > 300ms | 08:12 AM
[ALERT] core-switch-floor3 | Packet loss 4.2% | 09:45 AM
[ALERT] ap-conf-room-b | Client disconnections | 09:50 AM
[ALERT] ap-hallway-2 | Client disconnections | 09:52 AM
```

Without any guidance, the agent:

1. Pulled the alert history for `core-switch-floor3`
2. Noticed the latency issue had started before the packet loss
3. Recognized that the access point disconnections happened *downstream* of the same switch
4. Concluded that the switch was the likely root cause, not four separate problems
Its output looked like this:

> **Summary:** High-priority incident on core-switch-floor3 (Building A, Floor 3). Degraded performance beginning ~8:12 AM likely cascaded into packet loss and downstream client disconnections on two access points. This appears to be a single root cause, not isolated events.
>
> **Historical context:** This device has had 3 similar latency spikes in the past 6 months — all on Monday mornings, all resolved by restarting the uplink interface. Last occurrence: March 11, 2026. Resolved in 22 minutes by the network team.
>
> **Urgency:** High — affects conference room connectivity during business hours.
>
> **Suggested fix:** Restart uplink interface on core-switch-floor3 (worked in all 3 prior incidents). If issue persists beyond 15 minutes, escalate to network team lead and check for firmware updates flagged in the February maintenance log.

The room got quiet for a second. That's the kind of analysis that usually takes a network engineer 15-20 minutes to piece together. The agent did it in seconds.

---

## What Surprised Us

**The agent was better at correlation than we expected.** We assumed we'd need to hand-hold it with explicit logic. Instead, Gemini's reasoning handled the "connect the dots" work naturally once it had the right tools and context.

**Prompt engineering still matters — a lot.** The system prompt we gave the agent shaped everything. Early versions were too verbose, too cautious, or missed the urgency dimension entirely. Getting the tone and structure of the output right took as much iteration as the code itself.

**Tool design is the real architecture.** The most important decisions weren't about the agent — they were about what tools we gave it and what data those tools returned. Garbage in, garbage out still applies. Well-structured tool outputs made the agent dramatically smarter.

**It handled ambiguity better than rule-based systems.** Traditional alert correlation systems need explicit rules: *if X and Y occur within Z minutes, flag as related.* The agent could reason about novel combinations it had never seen before, which felt genuinely different.

---

## What We'd Build Next

We barely scratched the surface in a single hackathon day. The natural next steps would be:

- **Slack / Teams integration** — agent posts briefings directly to an on-call channel
- **Feedback loop** — engineers mark summaries as accurate/inaccurate, improving the agent over time
- **Auto-escalation** — for critical alerts, the agent drafts a ticket or pages the right person automatically
- **Multi-source ingestion** — pulling from ManageEngine, Statseeker, and SD-WAN vManage simultaneously for a unified view across the network stack

## The Bigger Picture

What struck me most about this hackathon wasn't the technology — it was how quickly a small team could build something *genuinely useful* with Google ADK and Gemini.

We're at a point where the gap between "interesting demo" and "solves a real problem" is narrowing fast. Network alert triage is just one example. The same pattern — agent ingests noisy data, uses tools to gather context, reasons about root cause, surfaces a clear recommendation — applies to security operations, customer support, IT helpdesk, financial monitoring, and more.

The agents aren't replacing the experts. They're doing the exhausting first pass so the experts can focus on the decisions that actually need human judgment.

That feels like the right division of labor to me.