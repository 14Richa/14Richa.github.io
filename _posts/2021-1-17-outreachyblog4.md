---
layout: post
title:  "Outreachy Week 7"
author: "Richa"
---


## Halfway to the internship’s progress report 

This blog includes a progress report of all that I’ve accomplished in the first half of the Outreachy internship. 

I’m so glad that I’ve successfully completed my week 7-8 on Outreachy. It was an awesome journey till now along with my mentors. Actually, Outreachy is a great community offering internships to underrepresented groups all around the world by working remotely and I love such platforms so much. It really encourages me to contribute to open source with freedom and to gain more knowledge.

### My role as an intern!

The project I am working on currently involves improving Firefox to give users more control over add-ons/ extensions in Container tabs. As we know Firefox Containers are a way for users to isolate their online identities and tasks from one another.

### Long description of the Project 

This project brings together two popular user-facing features of Firefox:

- Firefox add-ons can be installed by users to add more features to their browser. These extensions change the behavior of the browser and/or specific websites. Documentation for extension developers is available at https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions.

- Container tabs allow Firefox users to isolate browsing sessions within Firefox. This isolation of browsing sessions allows a user to separate their identity in some tabs from the rest of the browser. This feature is built into Firefox but disabled by default, and can be enabled by installing the Firefox Multi-Account Container add-on, or any other add-on that offers management of identities through the contextualIdentities extension API. These identities can be created and removed at any time.

Once installed, an add-on can be activated on every web page. Some users need to temporarily disable an add-on for a specific website or tab. This is currently not possible. The closest option is to either completely disable the add-on, or to limit its access to Private Browsing windows.

 These improvements would enable the following example user scenarios:
- Disabling "entertainment" extensions for work-related websites in the Work container.
- Disabling a spell checker extension in an online learning environment.
- Activating a price checker extension in the Shopping container only.
- Do online banking in the Bank container without any extensions.



The first half of my internship involved working on one of the widespread API  (Tabs API) and writing unit tests for the same. By saying it widespread I mean Tabs API will itself cover most of the extensions.  With the help of mentors (Rob and Luca) I have completed the Tabs API in the first half of the internship. Now, after discussing with my mentoresplan is to start a new API (webNavigation).

Currently, I am writing unit tests which are new to me. So, it is taking time but with the help of my mentors I know I will be able to do the same by the end of this week. And then start with the rest of the API’s.

At last, again I’d like to thank outreachy and Mozilla team for giving me the opportunity for such a great journey
