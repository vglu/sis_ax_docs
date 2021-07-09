# Development process

## Roles in implementation project

During implementation project usually we have different roles in project

|Role|Description|
|Developer||

## Stages of developmet during implementation project

During implementation project we touch with 2 stages.

### First stage - before go live

#### List of environments

First stage is stage when product not in `Live` yet, or we already in `Live` but with full support for all issues/bugs (usually very short period with full support Go Live process from implementation team)
We have this list of environments

| Name          | Description                                                                                                 |
| ------------- | ----------------------------------------------------------------------------------------------------------- |
| Dev1..n       | Environment use for development purpose. All modifications, bug fixes, ect                                  |
| Build-DEV     | Environment use for build code before check in. It can be one or few depends of needs                       |
| TEST(INTTEST)<sup id="a1">[*](#f1)</sup>| Environment use for testing by consultants modifications (optional, mostly used if every night build works) |
| TEST          | Environment use for testing by consultants modifications                                                    |
| UAT           | Environment use for testing by client modifications                                                         |
| GOLD          | Environment use for setup parameters for all modules. Used as template for Live                             |
| Live          | Environment use real work                                                                                   |
| DEMO<sup id="a1">[*](#f1)</sup>         | Usually with standard contoso data, can be used for demo purpose for clients (optional)                     |
| DM<sup id="a1">[*](#f1)</sup>           | Used for data-migration and testing data-migration procedure (optional)                                     |
| Sandbox<sup id="a1">[*](#f1)</sup>      | Used for some investigations purpose (optional)                                                             |

<b id="f1">*</b> optional [↩](#a1)

Allow to use any names but we recommend follow name convension from this list. Acceptable to use some prefixes and/or suffixes, but from name we should stronly understand what is this environment and what is the use case to use it. Good practice is to have full list of environments (in Azure DevOps wiki) with full description of environment purpose, owners (in case of DEV env), who order this environment, description of data on each environment. Also need to plan procedure to periodical check and refresh information in this wiki page.

#### Code live cycle

For any reason we want to extend existing functionality. In this case consultant should agree changes with process owner, write functional design document (FD/FDD). 
### Second stage - after go live

