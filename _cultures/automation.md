---
title: "Automation"
date: 2018-11-18T12:33:46+10:00
weight: 2
---


Over time, we've established various workspace automation to boost our productivity and easily access the information we want to learn.

Most automation centers around the following principles:
1. We want to diversify tools and workflows based on personal and team preferences to be productive.
2. We need to funnel all the information from various channels back to the most adopted platform (Slack).

## [Updates](https://github.com/EQWorks/updates)

Where can we best capture work progress? We attempt to source them from where work happens.

Our [`updates`](https://github.com/EQWorks/updates) project obtains activities from where work happens (GitHub) and where journals are kept (Notion). It then formulates the information into daily updates and weekly digests and sends to dedicated Slack channels for teammates to infer each others' whereabouts asynchronously.

![updates](https://user-images.githubusercontent.com/2837532/138357655-29d05974-25c2-4af5-93f7-f6f1d2dd388d.png)

## [Release](https://github.com/EQWorks/release)

Based on our [git conventions](git.md), we have developed [a CLI](https://github.com/EQWorks/release) (command-line interface) and an NLP (natural-language-processing) model to formulate release notes based on commit messages automatically.

You can read more about this in our blog post, ["Road to Automation: Release Notes."](https://medium.com/locus-engineering/road-to-automation-release-notes-d1c49cc97d9)

## [commit-watch](https://github.com/EQWorks/commit-watch)

Commit-watch is [another CLI](https://github.com/EQWorks/commit-watch) based on our git practices. The CLI helps us enforce the commit message conventions, which prepares the repository for better release notes materials.

## [scan-env](https://github.com/EQWorks/scan-env/)

Scan-env is a CLI to scan and alert environment variable usages in a git repository.

![scan-env](https://user-images.githubusercontent.com/2837532/138359803-57dca4b3-915c-4542-8b88-72a0a0f0f3da.png)

We often use `scan-env` and other routine CI (continuos-integration) and CD (continuous-deployment) processes to prevent environment variable-related runtime issues.

## [Legion](https://github.com/EQWorks/legion)

Our slash commands automation is driven by the [legion](https://github.com/eqworks/legion) project, our group chatbot.

### `/bday`
This command has three variants:
* `/bday sign` - sends a bday card link company-wide, excluding the bday person, as a slack direct message. To be used in the `#general` channel.

    <img src="https://user-images.githubusercontent.com/53827690/104040829-25786400-51a6-11eb-998a-2f1e24918f05.png" alt="/bday sign" width="30%" />
    <img src="https://user-images.githubusercontent.com/53827690/104041147-97e94400-51a6-11eb-9b45-53983c16cc24.png" alt="/bday sign msg" width="50%" />

* `/bday send` - sends the bday card to the bday person as a direct message in Slack.

    <img src="https://user-images.githubusercontent.com/53827690/104040892-37f29d80-51a6-11eb-9393-a37d9c7b2cf5.png" alt="/bday send" width="30%" />
    <img src="https://user-images.githubusercontent.com/53827690/104041103-86a03780-51a6-11eb-8407-d58a9aba40e8.png" alt="/bday send msg" width="50%" />

* `/bday celebrate` - triggers a bday message for the bday person. To be used in the `#general` channel.

    <img src="https://user-images.githubusercontent.com/53827690/104041034-67a1a580-51a6-11eb-9828-dff0162e70b1.png" alt="/bday celebrate" width="80%" />

### `/demo`

This command will add an event to the [demo calendar](https://calendar.google.com/calendar/u/0?cid=Y18wZGdoZ3MyNWo3cWplNmFhZmw0NDhybXQxY0Bncm91cC5jYWxlbmRhci5nb29nbGUuY29t) that the `/diff` outcome will then highlight.

<img src="https://user-images.githubusercontent.com/53827690/104034946-89e3f500-519f-11eb-8f4a-8b8d77d5ff78.png" alt="/demo" width="80%" />

### `/diff [product]` - Check product deployment difference between stages

This command complements our staged deployment practices for various products (such as front/back-ends of LOCUS and ATOM). It also utilizes the [`release` CLI](https://github.com/EQWorks/release) to classify commits and highlight critical contributors. With this information, the teams know who to approach for release consensus and provide follow-up supports for potential 0-days issues.

<img src="https://user-images.githubusercontent.com/53827690/104041420-01695280-51a7-11eb-9371-b8353880c07d.png" alt="/diff" width="80%" />

### `/release <product> [stage]` - Release product for deployment to a stage

This command automates the usual tagged release convention based on our git practices, combined with the usage of the `release` CLI to generate the release notes for the matching deployment.

The command is often paired right after running `/diff` and gathering consensus and discussions with involved contributors.

![/release](https://user-images.githubusercontent.com/2837532/138361306-c6505d18-a2ca-489d-91f7-a07c9ea5a00b.png)

### `/pipeline` - Data pipeline commands (currently checks capacity)

This commands taps into our AWS Data Pipeline to see its current capacity.

![/pipeline](https://user-images.githubusercontent.com/2837532/72271944-cf55fc80-35f5-11ea-971c-e75a55148e67.png)

### `/food` - Suggest restaurants

This commands leverages Yelp APIs to pull information of restaurants near the requested location. By default, it checks for ones near the EQ Works office.

![/food](https://user-images.githubusercontent.com/2837532/72272009-e98fda80-35f5-11ea-8dfc-e5ccb8d17797.png)
