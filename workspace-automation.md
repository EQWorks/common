# Workspace Automation

Over time, we've established various workspace automation to boost our productivity and easily access the information we are interested in.

## Asana

Automation on Asana projects is driven by [avail-bot](https://github.com/EQWorks/avail-bot), the bot runs routined workflows to interact with Asana API, and is also the bot that powers methods used behind our slack `/avail` command.

### Dev Avail

Asana Dev Avail project is listed under our Asana Dev team section. This project specifies our teammates' availability for each work day. Availabilities are being categorized as one of `Vacation`, `Remote`, `Office`, or `Not Avail (not able to work)`. Our `avail-bot` will run a daily routine to create & assign an availability task on Dev Avail for every dev, as well as marking them completed when the new cycle begins.

This Project helps to inform teammates of each other's availability status, the statuses could be configured either on Asana or using our slack `/avail` command.

### Dev Journal

Asana Dev Journal project is listed under our Asana Dev team section. This project provides an interface for devs to use as a general journal entry where they would note down their tasks for the day, usually written in to-do format. 

Our `avail-bot` runs a daily routine to create & assign dev-journal tasks for those who uses the journal. This automation formats completed prev-day subtasks into current day's `Last Workday` section, and incompleted prev-day subtasks will be re-created under the current day's subtasks section. This way, devs could could start their work by jumping right into left-over tasks from the previous day, and eliminates the tedious work of copy/paste prev-day taks to format current day's journal.

Dev Journal is a project that helps to inform teammates of what each other is currently working on, providing a general scope of active projects among all teams. These daily updates will also be captured into weekly digests used to generate our meeting notes. Consult our [journal guidelines](communications/journal.md) for more details.

## Slack Slash Commands

Our slash commands automation is driven by [legion](https://github.com/eqworks/legion), our group chatbot.

### `/avail` - Checks who is where

This command complements our `Dev Avail` Asana project. In this project, each team member specifies their availability status, with optional details. This allows us to check each others' availability status without interruption.

How it looks like in Slack:
![/avail](https://user-images.githubusercontent.com/2837532/72271739-725a4680-35f5-11ea-84c3-b7dfb8f082ed.png)

### `/bday`
This command has 3 variants:
* `/bday sign` - sends a bday card link company wide, excluding the bday person, as a slack direct message. To be used in the `#general` channel
* `/bday send` - sends the bday card to the bday person as a direct message in slack
* `/bday celebrate` - triggers a bday message for the bday person. To be used in the `#general` channel

How it looks like in Slack:
![/bday sign](https://user-images.githubusercontent.com/53827690/104040829-25786400-51a6-11eb-998a-2f1e24918f05.png)
![image](https://user-images.githubusercontent.com/53827690/104041147-97e94400-51a6-11eb-9b45-53983c16cc24.png)
![/bday send](https://user-images.githubusercontent.com/53827690/104040892-37f29d80-51a6-11eb-9393-a37d9c7b2cf5.png)
![image](https://user-images.githubusercontent.com/53827690/104041103-86a03780-51a6-11eb-8407-d58a9aba40e8.png)
![/bday celebrate](https://user-images.githubusercontent.com/53827690/104041034-67a1a580-51a6-11eb-9828-dff0162e70b1.png)


### `/demo`

This command will add an event to the [demo calendar](https://calendar.google.com/calendar/u/0?cid=Y18wZGdoZ3MyNWo3cWplNmFhZmw0NDhybXQxY0Bncm91cC5jYWxlbmRhci5nb29nbGUuY29t) that will then be highlighted by the `/diff` outcome.

How it looks like in Slack:
![/demo](https://user-images.githubusercontent.com/53827690/104034946-89e3f500-519f-11eb-8f4a-8b8d77d5ff78.png)
![failure](https://user-images.githubusercontent.com/53827690/102805433-38f39480-4389-11eb-9251-210d1efb40d0.png)
![success](https://user-images.githubusercontent.com/53827690/102805457-3e50df00-4389-11eb-8af6-acec2b4fcc9a.png)
![diff](https://user-images.githubusercontent.com/53827690/104042016-e519e580-51a7-11eb-8650-0aff607a0873.png)

### `/diff <product>` - Check product deployment difference between stages

This command complements our staged deployment practices for various products (such as front/back-ends of Locus and ATOM).

How it looks like in Slack:
![/diff](https://user-images.githubusercontent.com/53827690/104041420-01695280-51a7-11eb-9371-b8353880c07d.png)


### `/food` - Suggest restaurants

This commands leverages Yelp APIs to pull information of restaurants near the requested location. By default, it checks for ones near the EQ Works office.

How it looks like in Slack:
![/food](https://user-images.githubusercontent.com/2837532/72272009-e98fda80-35f5-11ea-8dfc-e5ccb8d17797.png)

### `/notes`

This command will compile messages in a thread as a Summary per project. It has 2 variants `/notes template` and `/notes <link>`. The latter requires the parent link of the thread (usually the one generated by Hugo note automation).

How it looks like in Slack:
![/notes template](https://user-images.githubusercontent.com/53827690/104035553-4473f780-51a0-11eb-8aed-468b93409d1c.png)
![/notes <link>](https://user-images.githubusercontent.com/53827690/104035787-89982980-51a0-11eb-998b-9059922f4477.png)

### `/pipeline` - Data pipeline commands (currently checks capacity)

This commands taps into our AWS Data Pipeline to see its current capacity.

How it looks like in Slack:
![/pipeline](https://user-images.githubusercontent.com/2837532/72271944-cf55fc80-35f5-11ea-971c-e75a55148e67.png)
