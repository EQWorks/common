# Journal

Dear Diary,

Yesterday, I did yet another batch of GAM segments upload, and re-re-mirrored swarm repo, again.

But enough with the chores, let me share with you something more exciting!

I finally further automated the GAM segment upload process to source newly submitted jobs from `segment_gam` data table. Even better, now OPs have learned to use the already built (albeit hidden) LOCUS UI (`/segments-gam`, and `/segments-gam-list`) to input the GAM List ID and Segment pairs. 100% win-win for all!

On the front-end of LOCUS (snoke), I finally completed this iteration of builder view job redesign implementation, as well as the builder list redesign follow-up issue (snoke#703). At last, the crawling is over.

On the back-end of LOCUS (first order), I upgraded the runtime to Node.js v12 across configurations including AWS Lambda, GitHub Actions, and local development environment (`.nvmrc`). This has the implication of reduced odd issues seen by developers who run different versions across projects and unknowingly run into mysterious GC/malloc related crashes. Feature-wise, maps list endpoint now filters out ones without a FINISHED job -- one less awkward "technical difficulties" for sales people to run into.

Also, our beloved common sees another addition of dedicated meetings section to offer both core objectives to pursue after, as well as practical guides for teams to adopt and adapt in order to achieve those objectives. Hope all teams that read and adopt it become better at do(dg)ing meetings ;)

Today, I plan to:
- Document on journal (:yodawg:), so everyone can get a better understanding of why we're doing this (perhaps not in a "Dear Diary" fashion).
- Come up with potential automations to make journal practices a bit less cumbersome, or a bit more insightful.
- Implement backoff retry logic for avail-bot routine so we don't shoot ourselves in the foot for evangelizing Dev Avail only to see it fail.
- Investigate snoke webpack dev server's insane CPU usage issue.
- ...

But obviously you know very well that I probably won't finish all, if any of the above. Let's keep out fingers crossed for no

Until the next work day.

Some Random Corporate Minion

YYYY-MM-DD HH:mm:ss+00:00

## Objectives

- Journals help you organize thoughts, and recollect memory.
- They give your teammates more context of where you have been.
- The evolving plan component offers your teammate insights of the direction you're heading toward.

## First Principle - Last Work Day

The first and most important principle is to write down what you have done in the _Last Work Day_, as comprehensively, and concisely, as possible.

We can be much better at our planning by reinforcing and associating back to what we have done.

This also allows others in the team to know what you have been doing, so that more efficient collaboration can be formed from this knowledge.

## Second Principle - Today's Plan

For _today's_ plan, carry over the leftovers from the last work day as a base and revise.

Keep the plan open, as the day ahead isn't 100% predictable, adjust it as you go.

This allows others in the team to know what you are doing, or about to be doing. This also opens up opportunities for more collaboration, and reduces the possibility of crossing over tasks unknowingly, or reinventing wheels unnecessarily.

## Third Principle - Break It Down

Try to break your plan down to smaller todos.

The purpose of this is to help _you_ to resolve problems in a more manageable manner, and give your morale a boost when you can cross off those todos in fabulous streaks.

This offers concrete insights for your team to understand your progress, instead of opaquely from 0% to 100%.

## Implementation Guide

One possible implementation is through an Asana project, like below:

<img width="1493" alt="asana" src="https://user-images.githubusercontent.com/2837532/76674485-699ad800-6586-11ea-8b5a-53ff36b4ce6d.png">

In it, each team member is responsible to create a daily "task" that serves as a container to host "Last Work Day", "Today's Plan" (in the form of Subtasks), and "due date" being only an association to _that_ day, such as the example below:

<img width="911" alt="journal" src="https://user-images.githubusercontent.com/2837532/76674353-f47ad300-6584-11ea-84f0-f3a6aba36840.png">

Furthermore, the "break it down" principle could be implemented through sub-subtasks:

<img width="911" alt="subtask" src="https://user-images.githubusercontent.com/2837532/76674360-03fa1c00-6585-11ea-8c98-47bbcdce1abb.png">

Every day at 10AM UTC time, a bot script runs to "Mark Complete" for all past "tasks" to shift everyone's attention to _today_.

## Potential Improvements

- A scheduled reminder (in group chat, or email) to notify every team member to compose _today's_ task.
- The reminder routine may also auto-create _today's_ task for each person, and the reminder content can be just the link to the Asana task itself.
- The reminder may parse through each person's _yesterday's_ task, carry over unfinished portion as the initial subtasks for _today_, and the finished portion into the _Last Work Day_ field. This should reduce nearly 90% (totally randomly guessed) of the chore feeling while doing this.

Before we could achieve these improvements, it is 100% doable by everyone, it only requires no more than 5 minutes at the beginning of the work day, some discipline, and a common agreement toward an overall better and more collaborative work environment.
