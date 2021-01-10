---
layout: post
title:  "Outreachy Week 5"
author: "Richa"
---


### Improve Firefox to give users more control over add-ons in Container tabs.

<br/>
Firefox Containers are a way for users to isolate their online identities and tasks from one another. In addition to the privacy benefits of containers, they also allow users to be logged into multiple accounts at once without requiring them to use multiple browsers or constantly sign in and out.

The project I am working on is about improving Firefox to give users more control over add-ons, by offering users the ability to selectively enable or disable add-ons in containers. These improvements would enable the following example user scenarios:

- Disabling "entertainment" extensions for work-related websites in the Work container.
- Disabling a spell checker extension in an online learning environment.
- Activating a price checker extension in the Shopping container only.
- Do online banking in the Bank container without any extensions.

The project's primary tasks are:

- Improve the internals of the extension framework to support isolation by containers.
- Extend existing extension APIs to support container-specific functionality.
- Develop a mechanism and a user interface to allow users to toggle add-ons in containers.

This project will yield a feature that allows Firefox users to get more control over what browser extensions run on specific groups of websites. This offers benefits in the form of more privacy and user agency, packed in a convenient feature.
