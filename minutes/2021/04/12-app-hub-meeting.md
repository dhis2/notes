When: Monday, 12 April, 2021
Who: Austin, Viktor, Birk, Médi, Debora, Phil, Radoslav

## Agenda

[#255](https://github.com/dhis2/notes/discussions/255)

- [Review Submitted Apps](https://docs.google.com/spreadsheets/d/1gdIyBM3e5zk9LtsqfEARyI59PVU2UfUvpaCJvLPkwMc/edit#gid=0)
  - [OMS / WHO relationship tracing app](https://apps.dhis2.org/user/app/474731e4-cd9b-4f7d-9075-6b1ee4c64ee8)?
  - Start review of legacy "approved" apps
- App Hub improvements
  - (devops) AWS deployment pipeline
  - (devops) error analytics, uptime monitoring?
  - (devops) process for database backups, manual psql
  - Source Code Links mandatory?
  - Blog about new [security recommendations](https://developers.dhis2.org/docs/guides/apphub-guidelines#security)?
  - [Users migration](https://jira.dhis2.org/projects/HUB/issues/HUB-105)
  - (security) enforce app-meta match on upload (manifest version number, slug, id, developer, etc MUST MATCH what's in the App Hub DB)
  - We really should have App Hub email integrations (i.e. [HUB-17](https://jira.dhis2.org/projects/HUB/issues/HUB-17?filter=allopenissues)), should we spec this out?
- Continuous delivery
  - [Publish script](https://github.com/dhis2/app-platform/pull/532) ready to go?
  - Plan for application versioning, min/max versions on App Hub
  - Plan for core app uploads (team effort?)

## Notes (lightweight)

- **TASK**: Add guidance on app forks to App Hub guidelines (Debora + Austin)

- DevOps
    - Currently we deploy to Elastic Beanstalk
        - Potentially we should move to ECS / Firegate ?
    - We should use the Devops project on Jira
        - There is an AWS component for now
        - Should we add an AppHub component?  Probably soon
    - What to do about manual sql? - ok for now in exceptional cases only
        - Backups are handled by RDS
    - Error analytics & uptime monitoring
        - We should set up something like Sentry, rollbar, etc.
        - There are AWS services for this
- **DECISION**: Source code links should mandatory for App Hub submissions
    - **TASK**: Add to App Hub guidelines (Debora)
- **TASK**: Everyone review security recommendations, blog post end of week
- Users issue
    - **TASK**: Birk to create proposal next week
- We need to ensure that app manifest matched App Hub metadata
    - **TASK**: Create Jira issue for enforcement  this (Austin)
- **TASK**: Get all core apps onto the app hub by next week (use a "simple" approach to just create IDs and upload a "base" version like 0.0.0 ?) (proposal by Varl?)
- **TASK**: Draft version proposal for next week (Austin)
