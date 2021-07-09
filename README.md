# Build, deploy on D365fo

- [Build, deploy on D365fo](#build-deploy-on-d365fo)
  - [Glossary](#glossary)
  - [Development process](#development-process)
  - [Minimal setup Azure devops](#minimal-setup-azure-devops)
    - [Folder/branch creating strategy](#folderbranch-creating-strategy)
    - [](#)
- [LCS](#lcs)
  - [Setup development environment](#setup-development-environment)
  - [Create new model](#create-new-model)


Main goal of this documentation is describe step by step guide to make development in D365fo simple, clear and understandable. Full documentation and recomendations presented by Microsoft and different blogs. This site just only need to make clear some questions with more examples and usecases.

## Glossary

To make possible to understand each others we should dial about terms in our documentation. All terms provide information to agree requirements between team members indide project

Full list of terms you can find on this page [page](/glossary.md)

## Development process

Implementation project has several phases. Please find more detail information about ALM process in Microsoft docs site. In two words, we should understand new requirements to product, understand why standard functionality not cover this requirements, describe new functionality on FDD. Functional consultant agree with Key users business requirements, Dev team lead estimate necessary changes, FDD going to approval process. Aprroved FDD assigned to developer. Developer develop changes and assign document to Consultant testing, Consultant assign new modification to Key user test. Please find more detailed description on [Development process page](/development-process.md)

## Minimal setup Azure devops

To setup Azure DevOps need to go to [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/), login to Azure DevOps

![Login to Azure DEV](static/AzureDevOpsMinimalSetup001.png)

and create new project.

Select your organizations and press the "New button".

![Create new project](static/AzureDevOpsMinimalSetup002.png)

Setup basic parameters

![Create new project basic parameters setup](static/AzureDevOpsMinimalSetup003.png)

where

| #   | Field name        | Description                                                                               |
| --- | ----------------- | ----------------------------------------------------------------------------------------- |
| 1   | Project name      | Enter project name                                                                        |
| 2   | Description       | Enter project Description                                                                 |
| 3   | Visibility        | Select project Visibility                                                                 |
| 4   | Version control   | Select Version control system VSTS or GIT. Now and later all description will around VSTS |
| 5   | Work item process | Select Work item process based on standards on company                                    |
| 6   | "Create" button   | Press "Create" button to create a new project                                             |

Also need to create a new folders `Trunk`, `Trunk\DEV`, `Trunk\DEV\Projects`, `Trunk\DEV\Metadata` under Repository section

![Create new trunk folder](static/AzureDevOpsMinimalSetup004.png)

![Folder created](static/AzureDevOpsMinimalSetup005.png)

Also we should convert `DEV` folder to branch. This and all other setup we run in DEV box.

### Folder/branch creating strategy

We can have any folders/branch name and can create it for each our needs. Microsoft only suggest to use `Main` folder/branch for environment upgrade, all others is depends of our needs. However, working from many different project better to use understandable and clear name for each folder/branch. We are recommend to use name below for different purpose

|Name|Path|Purpose of use|
|---|---|---|
|Trunk|root|Common folder for collect all actual development|
|Main|Trunk\Main|Branch for already tested and released code. It uses for collect ready to release to UAT code|
|Dev|Trunk\Dev|Branch for collect code from developers VMs|
|Dev-Feature|Trunk\Dev-Feature|Branch for collect code from developers VMs working under add new features |
|Main-Feature|Trunk\Main-Feature|Branch for collect features code ready tested and ready to release|

### 
# LCS

LCS is a Live cycle service from Microsoft. This service is a web site <https://lcs.dynamics.com/>

![LCS login screen](/static/LCS-login-screen.png)

Main goal for this service allow to manage D365FO implementation projects and all aspects related to this project. Select or create new project and enter into it.

![LCS login screen](/static/LCS-select-project.png)

On gamburger menu most main options it is

- Cloud-hosted environments - list of managed environments in project
- Asset library - library with projects artifacts (database backups, update packages etc...)

![LCS login screen](/static/LCS-project-main-page.png)

Cloud-hosted environments allows to manage environments (create, destroy, start, stop, update, login etc)

![LCS login screen](/static/LCS-env-management.png)

Where

| #   | Description                                  |
| --- | -------------------------------------------- |
| 1   | Possibility to add new environment           |
| 2   | Possibility to destroy existing environment  |
| 3   | Edit environment                             |
| 4   | Start/stop environment                       |
| 5   | Possibility to log on to D365FO              |
| 6   | Information about Azure connection           |
| 7   | Current selected environment                 |
| 8   | Credentions to login to environment over RDP |

## Setup development environment

All development is going on DEV boxes. One dev box designed for one developer. DEV box is a virtual machine. It can be placed on cloud and on premice as well. We will describe on cloud version only. DEV box it is already ready to work VM - All in one VM. It contain Visual studio installed, Dynamics 365 for finance and operations, MS Sql server, MS Office etc.

[How to deploy DEV box](/deploy-new-dev-box.md)

Login to DEV box

![Login to DEV box](/static/LCS-login-to-dev-box.png)

Where

| #   | Description                                         |
| --- | --------------------------------------------------- |
| 1   | Link do downloadable file with RDP setup connection |
| 2   | User for login to DEV Box                           |
| 3   | Password for user to DEV Box                        |

In DEV Box we should run Visual studio (current supported version 2017) as Administrator

![Open VS as administrator](/static/vs-open-as-administrator.png)

Enter credentials to Visual studio to continue work

When we open first time Visual studio we should setup our Azure DevOps repository. VS/menu/View/Team explorer.

![Connect to VSTS](/static/vs-connect-to-vsts.png)

Select existing connection or add new connection

![Connect to VSTS](/static/vs-connect-tovsts-select-server.png)

Select Advanced

![Connect to VSTS](/static/vs-vsts-change-workspace-setup.png)

And setup map between DEV box local resources and repository

![Advanced VSTS connect](/static/vs-vsts-advanced-workspace.png)

Agree with confirmation

![Advanced VSTS connect agree](/static/vs-vsts-workspace-sync.png)

For current moment we have setup VS code with our repository. If repository already has objects - its will synchronize when you press `Yes` button.

## Create new model