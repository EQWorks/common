# Workspace Automation

Over time, we've established various workspace automation to boost our productivity and get repetitive chores out of our way.

## Slack Slash Commands

Our slash commands automation is driven by [legion](https://github.com/eqworks/legion), our group chatbot.

### `/avail` - Checks who is where

This command complements our `Dev Avail` Asana project. The project allows our team to provide opt-in transparency of whether they are available to be contacted, in the form of physical presence in our office, or virtual presence remotely, on vacation, or not available.

How it looks like in Slack:
![/avail](https://user-images.githubusercontent.com/2837532/72271739-725a4680-35f5-11ea-84c3-b7dfb8f082ed.png)

### `/diff <product>` - Check product deployment difference between stages

This command complements our staged deployment practices for various products (such as front/back-ends of Locus and ATOM).

How it looks like in Slack:
![/diff](https://user-images.githubusercontent.com/2837532/72271864-af263d80-35f5-11ea-95ef-c85ef21b6a85.png)

### `/food` - Suggest restaurants

This commands leverages Yelp APIs to pull information of restaurants near the requested location. By default, it checks for ones near EQ Works office.

How it looks like in Slack:
![/food](https://user-images.githubusercontent.com/2837532/72272009-e98fda80-35f5-11ea-8dfc-e5ccb8d17797.png)

### `/pipeline` - Data pipeline commands (currently checks capacity)

This commands taps into our AWS Data Pipeline to see its current capacity.

How it looks like in Slack:
![/pipeline](https://user-images.githubusercontent.com/2837532/72271944-cf55fc80-35f5-11ea-971c-e75a55148e67.png)
