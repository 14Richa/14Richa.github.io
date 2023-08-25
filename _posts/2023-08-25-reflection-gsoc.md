---
layout: post
title: "Reflections on My GSoC 2023 Journey: My Achievements and What's Next with AsyncAPI Initiative"
author: "Richa"
---

In this blog post, I want to share what I did during Google Summer of Code 2023 with AsyncAPI Initiative.

During this program, I had the privilege of working with some amazing people who really helped me. I want to give a big shoutout to Lukasz Gornicki, KhudaDad Nomani, and Saurav Kumar for being great mentors. They guided me, supported me, and kept me motivated throughout the program.

Being a part of the AsyncAPI community has been a fantastic learning experience for me. I've gained so much knowledge, and working with this awesome group of people has been a truly memorable experience. In the upcoming sections of this blog post, I'll share the specific achievements that made my Google Summer of Code 2023 journey so special.

### Project Overview: [Automate paperwork around project governance](https://github.com/asyncapi/.github/issues/210)

The goal of my project was to automate the processes around project governance. This project aimed to automate the maintenance of the MAINTAINERS.yaml file, which contained the list of maintainers and TSC members of AsyncAPI. The tasks involved implementing workflows to automatically update the member's list based on changes in other files, inviting new maintainers and TSC members, updating the Emeritus.yaml file when someone was removed, and aggregating helpful information in the MAINTAINERS.yaml file. These automation and improvements made it easier to manage the maintainers and TSC members of AsyncAPI Initiative.

### Project Layout and Workflows

Before we get into the details of what I achieved, let's start with a visual overview of our project structure and workflows. You can see the full project layout and workflows in this [GitHub issue](https://github.com/asyncapi/community/issues/810)

We've used [Mermaid.js](https://14richa.github.io/2023-08-09/mermaid-lib) to create easy-to-understand diagrams that act like maps, showing how our project is organized and how different tasks are automated. These diagrams help us see how different parts of our project work together seamlessly.

Now, let's move on to the specific things I accomplished and contributed to during Google Summer of Code 2023 with the AsyncAPI Initiative.

### Successful Contributions

Before we get into the specific workflows I created, let me share how I started. I converted the TSC_MEMBERS.json file to the MAINTAINERS.yaml file to improve our project's structure. I also added a new key, `isTscMember`. You can review the details of this contribution [here](https://github.com/asyncapi/community/pull/720). 

Furthermore, I've added an Emeritus file, which lists individuals who were previously TSC members but are no longer active. You can find the details of this contribution in this [PR](https://github.com/asyncapi/community/pull/806).

Now, I'll provide insights into the workflows I developed during the program: 

-  `maintainers-tsc-changes-verification.yaml`

    This [workflow](https://github.com/asyncapi/community/blob/master/.github/workflows/maintainers-tsc-changes-verification.yaml) listens for changes to the MAINTAINERS.yaml file and ensures the validity of these changes. It differentiates between alterations made by bots and those made by humans. If a human modifies critical attributes or removes a maintainer object, the workflow blocks the pull request and notifies the user appropriately.
    
    - If the changes are made by an approved bot account, the pull request proceeds.
    - If human-made changes don't involve critical attributes, the pull request continues.


- `update-maintainers.yaml`

    This [workflow](https://github.com/asyncapi/.github/pull/248) actively monitors changes to the CODEOWNERS file and automatically updates the MAINTAINERS.yaml file accordingly. It also retrieves essential information like GitHub usernames, Twitter handles, and repository names from the API, notifying affected users. It selectively ignores changes related to bot accounts in the CODEOWNERS file.
    

- `tsc_management.yaml`

    This [workflow](https://github.com/asyncapi/community/blob/master/.github/workflows/tsc_management.yml) effectively manages changes to the tsc_members team and the Maintainers list within our project. It triggers when there is a change in the `isTscMember` property. In the event of an `isTscMember` property change, the workflow seamlessly adds or removes members from the TSC team based on the property's value. It also proactively notifies affected users when a member is added to the tsc_members team.

- `maintainer_management.yaml`

    This [workflow](https://github.com/asyncapi/community/blob/master/.github/workflows/maintainer_management.yml) comes into action when a pull request is closed in the repository. It focuses on managing alterations within the MAINTAINERS.yaml file, including additions, removals, or updates to maintainers.

    - When a pull request is merged, the workflow detects changes in the maintainers' list and takes appropriate actions.
    - If new maintainers are added, it sends invitations to join the organization and team, followed by a warm welcome message.
    - If maintainers are removed, it ensures their removal from the organization and conveys a goodbye message.
    - In cases of updates to TSC members, it diligently updates the Emeritus.yaml file to reflect these changes.

### Looking Forward

As my Google Summer of Code 2023 journey with the AsyncAPI Initiative approaches its conclusion in a few weeks, I'm taking a moment to reflect on the achievements and successes, but also to look ahead. It has been an incredible journey, and I'm enthusiastic about continuing to contribute and making our workflows even better.

- *Adapting to Real-World Scenarios and Enhancing Efficiency*

Testing is a critical aspect of workflow development. As we put our workflows into action, we may encounter new scenarios and test cases that we didn't initially anticipate. I will be working on fixes and adding more functionality based on testing and these real-world experiences.

- *Continuous Improvement and Bug Resolution*

The work we've done so far is just the beginning. Building automation workflows is an iterative process, and there's always room for improvement. I'm committed to continuously refining and enhancing the existing workflows. This involves closely monitoring their performance, identifying any bottlenecks or areas for optimization, and making the necessary adjustments to ensure they run seamlessly.