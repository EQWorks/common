# Meetings

Use the guides below as a starting point, and adapt for specific situations accordingly.

## Before A Meeting

Objectives:
- Determine the scope and minimum length of the meeting.
- Give all participants as much context as possible to make an informed decision on RSVP.
- Gather agenda items within the scope of the meeting
- Asynchronously resolve as many agenda items as possible before the meeting.

Guide for Organizers:
- Doublecheck the intended attendees to the meeting and ensure they have all received calendar invitations.
    - *Tip*: [How to use Zoom for meetings?](https://docs.google.com/document/d/1WNqeFKXYv_ji_PUXBKq8nlD09ErqmB6VoWasPW-BUDI/edit?usp=sharing)
- Initiate a **Meeting Note** on Hugo, provide as much context as possible. Sync it to a relevant Slack channel to prompt for pre-meeting discussions. ![notes-hugo](https://user-images.githubusercontent.com/2837532/104062313-3a65ef00-51c8-11eb-9a0c-005134c16473.png) ![notes-slack-thread](https://user-images.githubusercontent.com/2837532/103943174-9d3f8380-50ff-11eb-9377-b839d780e10a.png)
    - Make sure links to all relevant external references (such as Google Docs, Zoom recordings, Zeplin designs, Notion notes, etc.) are comprehensively included in the Hugo notes and make sure that all the participants have access to those.
    - *Tip*: Use Hugo's "New Note" instead of "Prepare" for meeting notes that are shareable to Slack channels that allow synchronized comments and thread replies.
    - *Tip*: Use Hugo's "Import Agenda" feature as a quick starting point for any meeting note, especially the one used for agenda discussions.

Guide for Participants:
- Go through relevant context, examples (where applicable):
    - Meeting notes and their associated pre-meeting discussions prepared by the organizer
    - Summary of pre-meeting discussions through the use of the [`/notes`](../workspace-automation.md#notes) command. ![notes-discussion-summary](https://user-images.githubusercontent.com/2837532/103942564-9bc18b80-50fe-11eb-9c3b-12dde574c43e.png)
    - Weekly digest (and daily updates) via the [automated updates feed](https://github.com/eqworks/updates). ![updates](https://user-images.githubusercontent.com/2837532/103942697-cb709380-50fe-11eb-8951-116c126e229c.png)
- Raise questions, proposals, and help resolve issues under the pre-meeting discussion thread. ![discussion](https://user-images.githubusercontent.com/2837532/103943386-feffed80-50ff-11eb-9fdf-16c5cbcfb3f5.png)

## During A Meeting

Objectives:
- Align & inform all participants of relevant information at the same time (synchronously).
- Maintain time for each agenda item & scope of meeting as intended.
- Record as many details as possible for future context/meetings.
- Crowdsource bookkeeping effort to increase accuracy, and minimize bias.

Guide for Organizers and Participants:
- Maintain timebox for agenda items.
- Try to demonstrate issues instead of abstractly talking about them.
- If certain agenda items cannot be resolved within the timebox, record all reasons and context into the meeting notes or discussion thread.
- Bookkeep through the same meeting notes (by organizers) or its discussion thread (by participants).
- Raise questions and additional proposals if time permits.
    - _Tip_: it's highly _recommended_ to do these [before the meeting](#before-a-meeting).

## After A Meeting

Objectives:
- Organize meeting notes to be as comprehensive as possible for both non-participants and future self.
- Determine suitable follow-ups for leftovers.
- Persist relevant information to a knowledge base.

Guide for Organizers and Participants:
- Add to the meeting note or its associated discussion thread with afterthoughts.
- If applicable, share the session recording to the relevant Slack channel(s).
- Summarize and derive actionable items from both pre-meeting and in-meeting notes.
    - Optionally create GitHub issues, Asana tasks, etc.
    - Utilize the [`/notes`](../workspace-automation.md#notes) slash command to roll up well-formatted content to help with the summarization.
- Set a time for a follow-up meeting if the scope of the leftover is complex.
