---
title: "Journals"
date: 2018-11-18T12:33:46+10:00
featured: true
weight: 1
---

# Journal

Journals don't always need to be like a ["Dear Diary" moment](https://gist.github.com/woozyking/fcb7e02c5babde022cc47352a606977b) (though it could be fun to write/read).

## Objectives

- Helps to organize thoughts and the recollection of daily tasks.
- Provides teammates with more context of what each other has been working on & gain insights on project direction.
- Feeds into weekly digests as a part of the meeting notes generation process.

## Workflow

### (1) Summarize Last Work Day

_Last Workday_ is a custom field in the journal:

<img width="799" alt="Screen Shot 2021-10-21 at 5 42 44 PM" src="https://user-images.githubusercontent.com/50936670/138361226-5ec0a1e6-d283-4ba0-b3ee-558d7f875ca1.png">

Notes in this section allow team members to know what you have been working on for better collaboration. Daily and weekly digests, powered by [updates](https://github.com/EQWorks/updates) that generate meeting notes also sourced from this section, so keeping them clear and concise is critical.

Our [avail-bot](https://github.com/EQWorks/avail-bot) routine for Dev Journal auto-fills _Last Workday_ with completed prev-day tasks. Please edit this section if you find any missing prev-day tasks or if they were poorly worded. You could revise these notes by directly typing them into the Last Workday section.

### (2) State Current Plan

State current plan as Subtasks. These subtasks then can be marked as completed as you progress:

<img width="948" alt="Screen Shot 2021-10-21 at 5 45 50 PM" src="https://user-images.githubusercontent.com/50936670/138361544-cb110acb-f579-4635-b151-e193f6e39d22.png">

Our [avail-bot](https://github.com/EQWorks/avail-bot) routine for Dev Journal takes over the prev-day incompleted tasks to the current workday as the base template, revise/add to the list accordingly.

Listing out current tasks updates teammates on what projects you are currently working on or about to start. This knowledge opens up opportunities for more collaboration, and it also reduces the possibility of crossing over tasks unknowingly or reinventing wheels unnecessarily.

Try to break your plan down to smaller to-dos whenever possible. Keep the plan open, as the time ahead isn't 100% predictable; adjust it as you go.

## Implementation Guide

Create your first journal as a page on Notion Dev Journal, and title the page with your name. Your journal page will appear alongside the journal pages of your teammates, like below:

<img width="1275" alt="Screen Shot 2021-10-21 at 5 37 59 PM" src="https://user-images.githubusercontent.com/50936670/138360595-d3c7ac98-dc0b-4793-97ba-979297de4214.png">

These pages on Dev Journal serves as a container to host the summary of _Last Workday_ and _Current Plan_ (in the form of _Subtasks_). Assign the page to yourself on the _Assignee_ field. The _Date_ field indicates the associated work session. The _Idle_ field will range from 1-5. The _Idle_ count will initiate if the prev-workday has no completed subtasks, and the count will increase on consecutive days of no activity. After five days of inactivity, the bot will no longer auto-create your journals.

<img width="1349" alt="Screen Shot 2021-10-21 at 5 41 18 PM" src="https://user-images.githubusercontent.com/50936670/138506773-8879a2ad-f5ea-4eee-b4c6-22b610c02bf4.png">
