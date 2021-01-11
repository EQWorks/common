# Journal

Journals don't always need to be like a ["Dear Diary" moment](https://gist.github.com/woozyking/fcb7e02c5babde022cc47352a606977b) (though it could be fun to write/read).

## Objectives

- Helps to organize thoughts and recollect memory of daily tasks.
- Provides teammates with more context of what each other has been working on & gain insights on project direction.
- Feeds into weekly digests as a part of the meeting notes generation process.

## Workflow

### (1) Summarize Last Work Day

_Last Workday_ is a custom field in the journal:

<img width="903" alt="Screen Shot 2021-01-08 at 4 57 20 PM" src="https://user-images.githubusercontent.com/50936670/104070132-24f6c200-51d4-11eb-9ff1-177fec31b192.png">

Notes in this section allows others in the team to know what you have been doing, so that more efficient collaboration can be formed from this knowledge. This section is also being sourced into weekly digests we generate for meeting notes, so it is key to keep them clear and concise.

Our [avail-bot](https://github.com/EQWorks/avail-bot) routine for Dev Journal auto-fills _Last Workday_ with completed prev-day tasks, please edit this section if you find any missing prev-day tasks, or if prev-day tasks were poorly worded. You could revise these notes by directly typing into the Last Workday section.

### (2) State Current Plan

State current plan as Subtasks, which could be marked as complete as you progress:

<img width="893" alt="Screen Shot 2021-01-08 at 5 05 42 PM" src="https://user-images.githubusercontent.com/50936670/104070164-3a6bec00-51d4-11eb-8898-c82077428d01.png">

Our [avail-bot](https://github.com/EQWorks/avail-bot) routine for Dev Journal carry over the prev-day incompleted tasks to current work day as a base, revise/add to the tasks accordingly.

Listing out current tasks allows others in the team to know what you are doing, or about to be doing. This also opens up opportunities for more collaboration and reduces the possibility of crossing over tasks unknowingly, or reinventing wheels unnecessarily.

Try to break your plan down to smaller todos whenever possible. Keep the plan open, as the time ahead isn't 100% predictable, adjust it as you go.

## Implementation Guide

Create your first journal as a task on Asana Dev Journal, and assign the task to yourself, like below:

<img width="1493" alt="asana" src="https://user-images.githubusercontent.com/2837532/76674485-699ad800-6586-11ea-8b5a-53ff36b4ce6d.png">

This self-assigned task on Dev Journal serves as a container to host the summary of _Last Workday_ and _Current Plan_ (in the form of _Subtasks_). _Due date_ is used to indicate when the work session is associated with.

<img width="911" alt="journal" src="https://user-images.githubusercontent.com/50936670/104071173-99cafb80-51d6-11eb-9869-409de5d225b1.png">

Furthermore, sub-subtasks can be used to further break larger plans/tasks down:

<img width="911" alt="subtask" src="https://user-images.githubusercontent.com/50936670/104070826-c9c5cf00-51d5-11eb-80b1-a2c27d81e263.png">

**Note**:
- Our automation bot will not carry over the sub-subtasks during the process due to Asana API rate limiting concerns as we loop through the tasks to fetch for its subtasks.
- Every day at ~10 AM UTC, the bot script also runs to "Mark Complete" for all past "tasks" to shift everyone's attention to the next _work day_.

