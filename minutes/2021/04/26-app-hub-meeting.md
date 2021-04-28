Who: Austin, Viktor, Joe, Médi, Birk, Debora, Phil
When: 2021-04-26 11:00 CET

## Agenda

Follow-up on [last meeting action items](https://github.com/dhis2/notes/blob/master/decisions/2021/04/19-app-hub-meeting.md)

## Notes

- [TASK] Versioning proposal for next week (Austin)
- [TASK] Update guidelines today (Austin, Debora)
- Empty apps (no version)
    - Some complexity around app version localization
    - Either 0.0.0 or wait for version proposal
    - Need to talk about how to migrate database
    - Should we have versioned descriptions?  Might be useful when features exist only in certain versons.
        - Encourage proper changelogs instead?
    - Replace per-version with per-app localization?
    - [TASK] Write up a migration proposal
- Priorities
    - 1 - enforcement fix [HUB-109](https://jira.dhis2.org/browse/HUB-109)
    - 2 - empty apps [HUB-111](https://jira.dhis2.org/browse/HUB-111)
    - 3 - upload core apps (v0 or empty)
- [TASK] ALL review the overhauled UI (https://redesign.eu-west-1.elasticbeanstalk.com/)
- [TASK] Create jira about app view/edit routes
    - DONE, created [HUB-112](https://jira.dhis2.org/browse/HUB-112)
- Org invitations with Amazon SES - Birk set up email notifications with Radislov
    - [DECISION] Use JWT for invitations, add some rate limiting (maybe just use SES)
    - [SUGGESTION] Stick with logging and alerting for now, add technical rate limiting in the future
