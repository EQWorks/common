# Workspace Automation

Over time, we've established various office automation to boost our productivity and gets repetitive chores out of our way.

## Slack Slash Commands

Our slash commands automation is driven by [legion](https://github.com/eqworks/legion), our group chat bot.

### `/avail` - Checks who is where

This command complements our `Dev Avail` Asana project. The project allows our team to provide opt-in transparency of whether they are available to be contacted, in the form of physical precense in our office, or virtual precense remotely, on vacation, or not available.

How it looks like in Slack:
[ss placeholder]

### `/diff <product>` - Check product deployment difference between stages

This commands complements our staged deployment practices for various products (such as front/back-ends of Locus and ATOM).

How it looks like in Slack:
[ss placeholder]

### `/food` - Suggest restaurants

This commands leverages Yelp APIs to pull information of restaurants near requested location. By default it checks for ones near EQ Works office.

How it looks like in Slack:
[ss placeholder]

### `/pipeline` - Data pipeline commands (currently checks capacity)

This commands taps into our AWS Data Pipeline to see its current capacity.

How it looks like in Slack:
[ss placeholder]
