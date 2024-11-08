[ ] Framework vs Methodology
[ ] classify all QA models and frameworks in a table
[ ] Preventive Quality Management:

# QC 360 Workshop - Holistic look at Quality

![Generic background image](hero.png '# QC 360 Workshop - Holistic look at Quality ' =400x400)

## Reason

This workshop is designed to foster a shared understanding of Quality Controls. We aim to demystify the processes and practices that underpin our commitment to excellence. Participants will gain insight into the risks, challenges, and mitigation strategies that are part of our daily efforts to ensure the highest quality in our software products. It's an opportunity for team members to engage, question, and comprehend the fundamental reasons behind our quality assurance methodologies and architectures, and to dive into the latest technologies and trends.

## Objectives

- Understand the different Quality Assurance models and methodologies.
- Explore the different stakeholders and their interests in the software development process.
- Understand the role of developers and QA engineers in the software development process.
- Understand the Xempus Playwright Architecture.
- Understand the importance of Business Processes and how they are modeled.
- Understand the Code-lifecycle and Controls.
- Understand the importance of UI Quality.
- Draft some viable improvement Goals and Plan of Action.

## Expected outcome

### Confluence Documentation

A detailed and interactive Confluence page that encapsulates a 360-degree view of our quality control process, serving as a dynamic resource for the team. This documentation will be a living document, updated regularly to reflect the latest insights and best practices.

//TODO: link to confluence page prepared

### Actionable Jira Tickets

//TODO: rules to create new tickets
// - labels
// - prises for most creator of tickets

Creation and assignment of Jira tickets to track and implement action items identified during the workshop, ensuring accountability and follow-through. These tickets will be prioritized and scheduled for completion within a specified timeframe.

### User Journey Review

A thorough examination and mapping of the entire user journey on Confluence using draw.io. We've dedicated three hours to collaborate on this task, aiming to visually outline each step and touchpoint. This exercise will help us identify gaps, redundancies, and opportunities for improvement.

//TODO: Miro board collaborative pre-prepared board

### Knowledge Sharing

An open platform for the team to share their expertise in QA, facilitating a collective upskilling and alignment of our Quality Assurance knowledge base. This knowledge-sharing session will be an opportunity for team members to present their insights, tools, and methodologies, fostering a culture of continuous learning and improvement.

//TODO: Knowledge Quiz

//TODO: Workshop feedback

## Index

- [QC 360 Workshop - Holistic look at Quality](#qc-360-workshop---holistic-look-at-quality)
  - [Reason](#reason)
  - [Objectives](#objectives)
  - [Expected outcome](#expected-outcome)
    - [Confluence Documentation](#confluence-documentation)
    - [Actionable Jira Tickets](#actionable-jira-tickets)
    - [User Journey Review](#user-journey-review)
    - [Knowledge Sharing](#knowledge-sharing)
  - [Index](#index)
  - [Agenda](#agenda)
    - [Day 1](#day-1)
  - [Topics](#topics)
    - [Welcome and Introduction](#welcome-and-introduction)
    - [Theory and concepts](#theory-and-concepts)
      - [QA in software development](#qa-in-software-development)
        - [Software QA models and methodologies (Quality Paradigms)](#software-qa-models-and-methodologies-quality-paradigms)
        - [There is more than 1 customer](#there-is-more-than-1-customer)
        - [Developers vs QA Engineers](#developers-vs-qa-engineers)
          - [What is software development](#what-is-software-development)
          - [Mindsets UML vs BPMN](#mindsets-uml-vs-bpmn)
    - [Xempus Playwright Architecture](#xempus-playwright-architecture)
      - [Behavior description (contract), Test Rationale, Test data, POM, Test Steps, Test Data, Test Results, Test Reports](#behavior-description-contract-test-rationale-test-data-pom-test-steps-test-data-test-results-test-reports)
      - [Gherkin vs Cucumber](#gherkin-vs-cucumber)
        - [Why we don't try Cucumber in Xempus](#why-we-dont-try-cucumber-in-xempus)
      - [Code lifecycle and pipeline / CI/CD](#code-lifecycle-and-pipeline--cicd)
    - [Business Processes](#business-processes)
      - [BPM \& BPMN](#bpm--bpmn)
      - [Test Traceability Matrix](#test-traceability-matrix)
      - [Manager Core Business Processes BPMN 2.0 (High level process flow)](#manager-core-business-processes-bpmn-20-high-level-process-flow)
      - [Code changing process](#code-changing-process)
    - [Code-lifecycle and Controls](#code-lifecycle-and-controls)
      - [Front-end](#front-end)
      - [Back-end / APIs](#back-end--apis)
      - [E2E - Playwright](#e2e---playwright)
      - [Systems monitoring (availability, performance, security)](#systems-monitoring-availability-performance-security)
      - [Code Repository configuration](#code-repository-configuration)
        - [.editorconfig file](#editorconfig-file)
        - [LICENSE file](#license-file)
        - [README.md file](#readmemd-file)
        - [CODEOWNERS.md file](#codeownersmd-file)
        - [.npmrc file](#npmrc-file)
        - [package.json file](#packagejson-file)
        - [Prettierrc file](#prettierrc-file)
        - [.eslintrc file](#eslintrc-file)
        - [.stylelintrc file](#stylelintrc-file)
        - [Project dictionary](#project-dictionary)
        - [vscode dictionary extension german plugin](#vscode-dictionary-extension-german-plugin)
      - [Linters and formatters](#linters-and-formatters)
        - [.editorconfig + .eslintrc + .stylelintrc + prettierrc](#editorconfig--eslintrc--stylelintrc--prettierrc)
      - [Convention and best practices](#convention-and-best-practices)
      - [Code Quality Metrics](#code-quality-metrics)
    - [UI Quality](#ui-quality)
    - [Design Systems](#design-systems)
      - [Accessibility (wai-aria)](#accessibility-wai-aria)
      - [Usability (UX, d3)](#usability-ux-d3)
      - [Performance (Google Lighthouse)](#performance-google-lighthouse)
    - [Draft some viable improvement Goals and Plan of Action](#draft-some-viable-improvement-goals-and-plan-of-action)

## Agenda

### Day 1

- 09:00 - 09:30: Welcome and Introduction
- 09:30 - 10:30: Total Quality Management (TQM)
- 10:30 - 11:00: Agile Testing Methodology
- 11:00 - 11:30: Six Sigma
- 11:30 - 12:00: Lean Software Development
- 12:00 - 13:00: Lunch Break
- 13:00 - 13:30: ISO 9001
- 13:30 - 14:00: Capability Maturity Model Integration (CMMI)
- 14:00 - 14:30: ITIL
- 14:30 - 15:00: Break
- 15:00 - 15:30: Icebreaker activity
- 15:00 - 16:00: Software QA models and methodologies (Quality Paradigms)

## Topics

### Welcome and Introduction

- Introduction to the workshop
- Overview of the workshop goals and expected outcomes: [Overview](https://www.youtube.com/watch?v=3vDWWy4CMhE) [7 mins]
- Icebreaker activity: [Two Truths and a Lie](https://www.youtube.com/watch?v=1J6R1Q6JQOw)
- Setting the tone for the workshop: [Setting the Tone](https://www.youtube.com/watch?v=3vDWWy4CMhE)
- Establishing ground rules and expectations: [Ground Rules](https://www.youtube.com/watch?v=3vDWWy4CMhE)
- Introduction to the facilitators and participants: [Introduction](https://www.youtube.com/watch?v=3vDWWy4CMhE)

### Theory and concepts

#### QA in software development

##### Software QA models and methodologies (Quality Paradigms)

Total Quality Management (TQM): [Total Quality management](total_quality_management.md) [1 hour]

Agile Testing Methodology: [Agile Testing Methodology](agile_testing_methodology.md) [20 mins]

Six Sigma: [Six Sigma](six_sigma.md) [30 mins]

Lean Software Development: [Lean Software Development](lean_software_development.md) [20 mins]

ISO 9001: [ISO 9001](iso_9001.md) [20 mins]

Capability Maturity Model Integration (CMMI): [Capability Maturity Model Integration (CMMI)](cmmi.md) [ 20 mins]

ITIL: [ITIL](itil.md) [20 mins]

##### There is more than 1 customer

- the end user vs the software architects [Square Hole video](https://www.youtube.com/watch?v=TNa-8tFoUxs)
  - all the stakeholders (it's jungle, not a church, not a market, not power rangers team) [there is in individuals, with their own goals and interests, and then there are the tribes, as well, with their own interests and goals] [matrix of stakeholders] [ individual interests, common interests and conflictive interests]
    - the business vs the developers
    - the business, the developers, the QA, the end user
    - the developers vs the QA
    - the QA vs the end user
    - the end user vs the business
    - the business vs the QA
    - the end user vs the developers
    - the developers vs the business
    - the QA vs the business

##### Developers vs QA Engineers

- sensitive [Project fights](https://www.youtube.com/watch?v=wi8yJdKO1j0)
- <https://www.youtube.com/watch?v=f-uoKSRfg44>
- become ruthless, have no feelings <https://www.youtube.com/watch?v=yVxJnWR5Rzw>

###### What is software development

- bpmn process
- process inputs (in software factory, sprints, etc)
- outputs (code, tests, documentation, etc)
- risks (security, performance, availability, etc)
  - risk assessment (risk assessment matrix)
  - risk matrix (likelihood, impact)
  - controls (preventive, detective, corrective)
    - cost of controls -> but we can automate them -> test automation + CI/CD + monitoring + alerting + logging + tracing + profiling + linting + formatting + reviews + pair programming + mob programming + TDD + BDD + DDD + etc.
  - risk mitigation (accept, transfer, avoid, mitigate)

###### Mindsets UML vs BPMN

- Theo on unit tests video [Why I don't Unit Test](https://www.youtube.com/watch?v=ZGKGb109-I4)
- Primaegen vs Theo [YOU DONT UNIT TEST??? DevHour #1 Theo](primaegen_unit_test.md)
- Primaegen on unit tests [Thoughts About Unit Testing | Prime Reacts](https://www.youtube.com/watch?v=KzV0mTqBcZA)
- The and Primaegen [We Finally Agree On Unit Tests](https://www.youtube.com/watch?v=MbU-PKukdMw)
- Test Pyramid (and Ice-cream cone) Models
- Generic Test Automation Architecture

---

### Xempus Playwright Architecture

#### Behavior description (contract), Test Rationale, Test data, POM, Test Steps, Test Data, Test Results, Test Reports

#### Gherkin vs Cucumber

The goal of Cucumber is to enable a business analyst to write a specification in plain text that can be executed as an automated test. The text is written in a business-readable domain-specific language and serves as documentation, automated tests, and development-aid - all rolled into one format.

The problem with Gherkin is that it is not a programming language, it is a domain-specific language. It is not a programming language because it does not have the ability to perform operations like loops, conditions, etc. It is a domain-specific language because it is designed to be used by non-programmers to write test cases.

But it enables the creation of a common language between the business and the developers, and it is a good way to document the requirements and the tests.

##### Why we don't try Cucumber in Xempus

It was tried in the past, //TODO: ask Hosnia what happened in the past

The complexity of systems, like "I go to the login page", which one? advisor-main, advisor-exclusive-agents, manager, consumer? and this only for the login page, what about the rest of the system?

#### Code lifecycle and pipeline / CI/CD

---

### Business Processes

#### BPM & BPMN

#### Test Traceability Matrix

#### Manager Core Business Processes BPMN 2.0 (High level process flow)

#### Code changing process

---

### Code-lifecycle and Controls

#### Front-end

#### Back-end / APIs

#### E2E - Playwright

#### Systems monitoring (availability, performance, security)

#### Code Repository configuration

##### .editorconfig file

The .editorconfig file is a configuration file that defines and maintains consistent coding styles across different editors and IDEs. It helps developers adhere to coding standards, such as indentation, line endings, and character encoding, by specifying rules in a simple format that can be read and understood by various tools.

[EditorConfig](editorconfig.md)

##### LICENSE file

The LICENSE file is a legal document that specifies the terms and conditions under which the software or project can be used, modified, and distributed. It helps protect the rights of the project creator and outlines the permissions granted to users regarding the usage of the codebase.

[Xempus Repo Licenses](LICENSE.md)

##### README.md file

The README.md file is a markdown file commonly found in software projects to provide essential information about the project. It serves as a documentation hub for developers, users, and contributors, offering details on how to use the project, installation instructions, configuration settings, and other relevant information.

//TODO: TBD
[README.md](README.md)

##### CODEOWNERS.md file

The CODEOWNERS.md file is a convention in Xempus to try to clarify who is responsible for reviewing and approving changes to specific parts of the codebase. This file helps streamline the code review process and ensures that changes are reviewed by the appropriate stakeholders before being merged into the main branch.

[CODEOWNERS.md](CODEOWNERS.md)

##### .npmrc file

The .npmrc file is a configuration file used by the Node Package Manager (npm) to customize and configure various settings for how npm behaves. This file can be located in the user's home directory or at the project level to override default settings.

[.npmrc](npmrc.md)

##### package.json file

The package.json file is a metadata file used by Node.js projects to define project dependencies, scripts, and other configuration settings. It provides essential information about the project, such as the project name, version, description, author, and dependencies, and helps manage project dependencies and scripts.

[package.json](package.json)

##### Prettierrc file

The .prettierrc file is a configuration file used by the Prettier code formatter to define coding styles and formatting rules for a project. It helps developers maintain consistent code formatting across the codebase and ensures that the code adheres to the specified style guidelines.

[Prettier](prettierrc.md)

##### .eslintrc file

The .eslintrc file is a configuration file used by the ESLint linter tool to define coding rules and standards for a project. It helps developers identify and fix code quality issues, enforce coding standards, and maintain code consistency across the codebase.

//TODO: TBD
[ESLint](eslintrc.md)

##### .stylelintrc file

The .stylelintrc file is a configuration file used by the Stylelint linter tool to define CSS and SCSS coding rules and standards for a project. It helps developers identify and fix style issues, enforce style guidelines, and maintain style consistency across the codebase.

//TODO: TBD
[Stylelint](stylelintrc.md)

##### Project dictionary

VS Code built-in dictionary + plugin + german dictionary + custom dictionary

##### vscode dictionary extension german plugin

#### Linters and formatters

##### .editorconfig + .eslintrc + .stylelintrc + prettierrc

How to deal with all the configurations without conflicts?

#### Convention and best practices

#### Code Quality Metrics

---

### UI Quality

### Design Systems

#### Accessibility (wai-aria)

#### Usability (UX, d3)

#### Performance (Google Lighthouse)

---

### Draft some viable improvement Goals and Plan of Action

Software QA models and methodologies (Quality Paradigms)
Total Quality Management (TQM)
Agile Testing Methodology
Six Sigma
Lean Software Development
ISO 9001
Capability Maturity Model Integration (CMMI)
ITIL
