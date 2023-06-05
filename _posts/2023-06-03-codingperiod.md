---
layout: post
title:  "My First Coding Week in GSoC with Postman and AsyncAPI"
author: "Richa"
---

I am delighted to share my experiences during the first week of my GSoC 2023 coding period with Postman and AsyncAPI. My coding period started on May 29th, 2023, and it has been an amazing community to be a part of. I am excited to contribute to the project in the coming weeks.

During my first week, I worked on creating flowcharts for the project using Mermaid, a powerful tool that offers a wide range of benefits for developers. I was impressed with its simple and intuitive syntax, wide range of diagram types, easy integration with Markdown, customizable styling, and real-time updates. It was an excellent choice for creating visual representations of my code.

In addition, I raised a [pull request](https://github.com/asyncapi/community/pull/719) for the flowchart, which was a great learning experience. My mentors and I have weekly sync calls to discuss the agenda, and I found that this helped me to stay on track and receive feedback on my progress.

In addition to the flowchart, I also contributed to the project by creating two workflows. The first workflow I created during my first week is called `Welcome New Contributor`. This [workflow](https://github.com/asyncapi/community/blob/master/.github/workflows/msg-to-new-member-pr-merged.yml) runs whenever a pull request is closed and the file "TSC_MEMBERS.json" is affected.

I'm happy to say that this workflow was merged into the project! :smiley:

The purpose of this workflow is to welcome new contributors to the project and help them get started. It includes several steps that check for changes to the file and compare it to the version in the main branch. If new contributors have been added to the file, the workflow sends a welcome message to each new contributor via a GitHub comment.

Through this workflow, I learned a lot about setting the head of a branch, checking for changes to files using GitHub actions, and sending notifications through GitHub comments. It was a great learning experience

Another workflow I created is `YAML Lint Check`. This workflow runs on every pull request to the master branch in the ".github/workflows" directory. Its purpose is to check all the YAML files in the directory for syntax errors and validate them against the GitHub Actions workflow schema. For example, you can see this workflow in action in this [pull request](https://github.com/asyncapi/.github/pull/238).

The workflow uses a tool called [yamllint](https://yamllint.readthedocs.io/en/stable/) to check for syntax errors. If any errors are found, the workflow fails. It also uses the [ajv](https://ajv.js.org/guide/getting-started.html) library to validate the YAML files against the schema. If any validation errors are found, the workflow fails.

This workflow is a great way to catch errors early in the development process and ensure that all YAML files in the ".github/workflows" directory are free from syntax errors and conform to the GitHub Actions workflow schema. It can save time and effort in the long run by preventing errors from propagating further down the development pipeline.

In addition to the workflows, I started working on migrating JSON to YAML and updating the website code to support the new format. This was a significant undertaking as it allowed for a smoother transition to YAML and improved the user experience. As part of this effort, I raised a pull request that was focused on this migration. You can find the PR for this contribution [here](https://github.com/asyncapi/website/pull/1722).

Overall, my first week in GSoC 2023 with Postman and AsyncAPI was an incredible learning experience. Working with an amazing team of developers, I gained valuable insights into open-source development, communication, and project management. I was impressed by the level of support and mentorship provided to help me succeed in my role.

I am eager to continue contributing to the project and exploring new technologies and tools. This first week has given me a sense of confidence and motivation to further develop my skills, and I am looking forward to the challenges ahead. I appreciate the level of support and mentorship that I have been receiving and I am grateful for the opportunity to be a part of a project.