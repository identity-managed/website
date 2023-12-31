---
title: a sprinkling of understanding Workflow in ILM 2
date: 2008-09-16T17:48:00.001-07:00
draft: false
url: /2008/09/sprinkling-of-understanding-workflow-in.html
description: Workflow in ILM 2 FIM MIM
tags:
  - Workflow
  - WWF
  - ILM 2 Beta 3
  - FIM
  - MIM
---
So by now all of you know that understanding Windows Workflow Foundation is going to be quite helpful in implementing ILM 2.

Having lived 9 of the last 12 months in Redmond, WA, I now understand a lot more about sprinkling

So I thought I would provide a sprinkling of understanding about Windows Workflow Foundation: a categorization of the built in workflows.

| Cateory     | Activity                   | Composite | Notes                                     |
|-------------|----------------------------|-----------|-------------------------------------------|
| Conditional | Invoke Web Service         |           |                                           |
| Conditional | Conditional Activity Group |           |                                           |
| Conditional | IfElse                     |           |                                           |
| Conditional | Policy                     |           | Akin to a switch statement or Select Case |
| Conditional | While                      |           |                                           |
| Custom      | Code                       |           |                                           |
| Error       | Compensate                 |           |                                           |
| Error       | Fault Handler              |           |                                           |
| Error       | Throw                      |           |                                           |
| Flow        | Delay                      |           |                                           |
| Flow        | EventDriven                |           |                                           |
| Flow        | Listen                     | X         | 2+ event driven                           |
| Flow        | Parallel                   | x         | 2+ sequence for each                      |
| Flow        | State                      |           |                                           |
| Flow        | Sequence                   | X         |                                           |
| Flow        | SetState                   |           |                                           |
| Flow        | StateInitialization        | X         |                                           |
| Flow        | Suspend                    |           |                                           |
| Flow        | Terminate                  |           |                                           |
| Flow        | Transaction Scope          |           |                                           |

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices