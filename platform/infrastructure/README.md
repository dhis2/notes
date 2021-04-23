<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [DHIS Cloud Infrastructure Strategy](#dhis-cloud-infrastructure-strategy)

- [DHIS Cloud Infrastructure Strategy](#dhis-cloud-infrastructure-strategy)
  - [Abstract](#abstract)
  - [Guiding Principals](#guiding-principals)
    - [IaC](#iac)
    - [Separation](#separation)
      - [Environments](#environments)
      - [Projects](#projects)
      - [Shared functionality](#shared-functionality)
    - [Access](#access)
    - [Instantiating of new infrastructure](#instantiating-of-new-infrastructure)
  - [Project structure](#project-structure)
    - [modules](#modules)
    - [platform](#platform)
    - [cache-cleaner](#cache-cleaner)
    - [other-app](#other-app)
  - [State](#state)
  - [Security](#security)
  - [AWS Accounts](#aws-accounts)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# DHIS Cloud Infrastructure Strategy

The following should serve as guidelines for implementing our cloud infrastructure.

It will forever be work in progress meant to fostering discussions which will hopefully lead to best practice decisions.

## Abstract
Inline with standard development principals we should start with a minimal viable product approach with focus on separation on concerns

## Guiding Principals

### IaC
Every piece of our infrastructure should be defined as code.

Defining infrastructure by clicking in the web UI or executing command line commands is prohibited.

### Separation
On one side we have environments such as dev and production which are important to separate. It's also relevant when it comes to the infrastructure of the individual projects. Does one project have the need to use a queue, or a database it should be defined locally.

#### Environments
The implementation should support multiple environments. Although we'll probably only run one production environment it's crucial that we're able to spin up an exact copy for the sake of development and testing.

#### Projects
Ideally each project should define its own infrastructure but initially a monolithic approach could be used.  
[Mono repo vs Multi repos debate](https://www.hashicorp.com/blog/terraform-mono-repo-vs-multi-repo-the-great-debate)

#### Shared functionality
Shared functionality should be implemented centrally as modules and shared across environments or projects.

### Access
Access should be granted per need in such a way that project members have access to their own infrastructure but not the infrastructure of other projects.

### Instantiating of new infrastructure
Requests for new infrastructure should be done through pull requests and follow standard development processes.

!!!### Scalability
!!!In order for our infrastructure development to scale and not be stuck on a specific technologies/versions for the entire organization the infrastructure for each project should implement in its own repository.

## Project structure
Initially we should keep everything in one repository and if that grows out of hand we could divide things into several smaller repositories. Starting with a `platform-infrastructure` repository and then expanding as needed could be a way.

???Every resource should have a postfix to its name indicating which environment it belongs to.

```
/modules/{network,users,storage}/{main.tf,vars.tf,output.tf}
/platform/{main.tf,vars.tf,output.tf}
/apps/cache-cleaner/{main.tf,vars.tf,output.tf}
/apps/other-app/{main.tf,vars.tf,output.tf}
```

### modules
Should contain our cross app/environment functionality used by multiple projects.

### platform
Should contain our main resources.

### cache-cleaner
Define DNS
Use module from modules to deploy on CDN

### other-app
Define DNS
Use module from modules to deploy on CDN 
S3?

## State
Initially use one bucket with multiple keys for the state of the platform and each app

## Security
???

## AWS Accounts
Does it make sense to use multiple accounts?
