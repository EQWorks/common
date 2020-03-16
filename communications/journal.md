# Journal

Journals don't always need to be like a ["Dear Diary" moment](https://gist.github.com/woozyking/fcb7e02c5babde022cc47352a606977b) (though it could be fun to write/read).

## Objectives

- Journals help you organize thoughts and recollect memory.
- They give your teammates more context of where you have been.
- The evolving plan component offers your teammate insights into the direction you're heading toward.

## Guide

### First Principle - Summarize Last Work Session

The first and most important principle is to write down what you have done in the _Last Work Session_ as comprehensively as possible.

We can be much better at our planning by reinforcing and associating back to what we have done.

This also allows others in the team to know what you have been doing, so that more efficient collaboration can be formed from this knowledge.

Adaptations:

- Sessions can be in different lengths, such as every day, every other day, or every week.
- However, it is better to have consistent session lengths. This allows members in collaboration with you to have a predictable period to check-in with you.

### Second Principle - State Current Plan

For the current work session, carry over the leftovers from the last work session as a base and revise.

This allows others in the team to know what you are doing, or about to be doing. This also opens up opportunities for more collaboration and reduces the possibility of crossing over tasks unknowingly, or reinventing wheels unnecessarily.

Keep the plan open, as the time ahead isn't 100% predictable, adjust it as you go.

Adaptations:

- Try to break your plan down to smaller todos whenever possible.

## Implementation Guide

One possible implementation is through an Asana project, like below:

<img width="1493" alt="asana" src="https://user-images.githubusercontent.com/2837532/76674485-699ad800-6586-11ea-8b5a-53ff36b4ce6d.png">

In it, each team member is responsible to create a "task" that serves as a container to host the summary of _Last Work Session_ (in this exampe, session length = one day) and the _Current Plan_ (in the form of _Subtasks_). _Due date_ is used to indicate when the work session is associated with.

<img width="911" alt="journal" src="https://user-images.githubusercontent.com/2837532/76674353-f47ad300-6584-11ea-84f0-f3a6aba36840.png">

Furthermore, sub-subtasks can be used to further break larger plans/tasks down:

<img width="911" alt="subtask" src="https://user-images.githubusercontent.com/2837532/76674360-03fa1c00-6585-11ea-8c98-47bbcdce1abb.png">

Every day at ~10 AM UTC, a bot script runs to "Mark Complete" for all past "tasks" to shift everyone's attention to the next _work session_.

## Potential Improvements

A bot script may parse through each person's _Last Work Session_ task, to do the following:
- Create a new _Current Work Session_ task that matches the previous session length.
- Move the unfinished subtasks as the initial subtasks for the current one
- Move the finished portion into the _Last Work Session_ field.
