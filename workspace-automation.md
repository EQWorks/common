# Workspace Automation

Over time, we've established various workspace automation to boost our productivity and easily access the information we are interested in.

## Slack Slash Commands

Our slash commands automation is driven by [legion](https://github.com/eqworks/legion), our group chatbot.

### `/avail` - Checks who is where

This command complements our `Dev Avail` Asana project. In this project, each team member specifies their availability status, with optional details. This allows us to check each others' availability status without interruption.

How it looks like in Slack:
![/avail](https://user-images.githubusercontent.com/2837532/72271739-725a4680-35f5-11ea-84c3-b7dfb8f082ed.png)

### `/diff <product>` - Check product deployment difference between stages

This command complements our staged deployment practices for various products (such as front/back-ends of Locus and ATOM).

How it looks like in Slack:
![/diff](https://user-images.githubusercontent.com/2837532/72271864-af263d80-35f5-11ea-95ef-c85ef21b6a85.png)

### `/food` - Suggest restaurants

This commands leverages Yelp APIs to pull information of restaurants near the requested location. By default, it checks for ones near the EQ Works office.

How it looks like in Slack:
![/food](https://user-images.githubusercontent.com/2837532/72272009-e98fda80-35f5-11ea-8dfc-e5ccb8d17797.png)

### `/pipeline` - Data pipeline commands (currently checks capacity)

This commands taps into our AWS Data Pipeline to see its current capacity.

How it looks like in Slack:
![/pipeline](https://user-images.githubusercontent.com/2837532/72271944-cf55fc80-35f5-11ea-971c-e75a55148e67.png)

## Asana

Automation on Asana projects is driven by [avail-bot](https://github.com/EQWorks/avail-bot), the bot runs routined workflows to interact with Asana API, and is also the bot that powers methods used behind our slack `/avail` command.

### Dev Avail

Asana Dev Avail project is listed under our Asana Dev team section. This project specifies our teammates' availability for each work day. Availabilities are being categorized as one of `Vacation`, `Remote`, `Office`, or `Not Avail (not able to work)`. Our `avail-bot` will run a daily routine to create & assign an availability task on Dev Avail for every dev, as well as marking them completed when the new cycle begins.

This Project helps to inform teammates of each other's availability status, the statuses could be configured either on Asana or using our slack `/avail` command.

### Dev Journal

Asana Dev Journal project is listed under our Asana Dev team section. This project provides an interface for devs to use as a general journal entry where they would note down their tasks for the day, usually written in to-do format. 

Our `avail-bot` runs a daily routine to create & assign dev-journal tasks for those who uses the journal. This automation formats completed prev-day subtasks into current day's `Last Workday` section, and incompleted prev-day subtasks will be re-created under the current day's subtasks section. This way, devs could could start their work by jumping right into left-over tasks from the previous day, and eliminates the tedious work of copy/paste prev-day taks to format current day's journal.

Dev Journal is a project that helps to inform teammates of what each other is currently working on, providing a general scope of active projects among all teams. These daily updates will also be captured into weekly digests used to generate our meeting notes. Consult our [journal guidelines](https://github.com/EQWorks/common/blob/master/communications/journal.md) for more details.
