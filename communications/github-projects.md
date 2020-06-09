## On Github Projects

Since the [Covid Dash development](https://github.com/EQWorks/flaat-dash/projects), we have been using github projects to keep track of progress, issues, and code-specific discussions due to the fast paced nature of the project. 

Github Projects tool can be used in any other repository. Repos can have multiple projects. Projects can be specific to one extensive task or the whole repo in general - ideally both. Projects that have issues intertwined with different repositories (for instance front-end repo and back end repo) can take advantage of the cross-repo issue referencing. 

<img width="800" alt="column" src=https://user-images.githubusercontent.com/53827690/83157518-b1cf8e00-a0d1-11ea-9b2c-7a4019ae5066.png>

Projects are shown as a kanban board so it's easy to keep track of progress. It automatically shows the percentage between open issues / completed issues.

<img width="800" alt="column" src=https://user-images.githubusercontent.com/53827690/83158139-6964a000-a0d2-11ea-9e37-b3f6edd0b7f4.png>

The project is fully customizable and the user can add or delete columns relevant to the project
<p align="center">
    <img width="300" alt="column" src=https://user-images.githubusercontent.com/53827690/83159389-ec3a2a80-a0d3-11ea-89fa-7e112f77747d.png>
    <img width="310" alt="column" src=https://user-images.githubusercontent.com/53827690/83159809-68cd0900-a0d4-11ea-8a00-d6bb168708bb.png>
</p>

#### On issues
An issue is created as a to-do item, assigned to a person and labeled:
- On the ToDo card, click `+`, add a title to your issue, and click `add` a note.
- Once the note is created, click on `...` of that new ToDo note and choose `convert to issue`.
- Click on the title of that issue now and a side card will pop on the right. Choose an assignee, add a description, add labels - multiple labels can be added according to the context of that issue.
- Move the issue between cards to update its status accordingly: when assigned to someone, move to `in progress`, when PR is up, move to `Review in progress`

![image](https://user-images.githubusercontent.com/53827690/83170748-00d1ef00-a0e3-11ea-8f38-ef07b7873671.gif)

Issues can belong to more than one project at the same time

<img width="200" alt="column" src=https://user-images.githubusercontent.com/53827690/83175039-4c879700-a0e9-11ea-94c7-806376db9c8f.png>

#### On Labels
Try to use labels to categorize issues and pull requests. There are template labels provided out of the box for each repository. One can also consider some of our own usage examples below:
- bug - of a feature that already exists
- layout/design - style modifications
- enhancement - improving an existing feature
- feature - creating a new functionality

#### On PR
Overall, same rules apply for PR, consult the [guides on Git](../git.md).

Specific to `Projects`, PR description should always refer to the issue because they will automatically close the issue and move the project progress once merged. The syntax to close the issue needs to use [keywords followed by the issue number](https://help.github.com/en/enterprise/2.16/user/github/managing-your-work-on-github/closing-issues-using-keywords#about-issue-references). e.g. `closes #100`

<img width="600" alt="column" src=https://user-images.githubusercontent.com/53827690/83160932-cca40180-a0d5-11ea-9924-b24bc8aca631.png>

Issues can be cross-referred to from different repos/projects.
To refer or close an issue from a different repo, the syntax is `username/repository#issue_number` e.g. `EQWorks/covidata#52`

<img width="600" alt="column" src=https://user-images.githubusercontent.com/53827690/83162499-d6c6ff80-a0d7-11ea-8037-4f4622c2fde4.png>


Depending on the project, it might be worth it to subscribe issues to the relevant slack channel so every time an issue is created or closed, a notification is sent to the relevant channel.
<p  align="center">
    <img width="400" alt="slack" src=https://user-images.githubusercontent.com/53827690/83161385-61a6fa80-a0d6-11ea-8cea-f0bce6bc9ac5.png>
</p>


## General references
- [GitHub Project](https://github.com/features/project-management/)