Who: Austin, Joe, Médi, Birk, Debora, Phil, Scott
When: 2021-04-19 11:00 CET

## Agenda

Follow-up on [last meeting action items](https://github.com/dhis2/notes/blob/master/decisions/2021/04/12-app-hub-meeting.md)

## Notes

- Added Source Code requirement to guidelines [here](https://github.com/dhis2/developer-portal/pull/13)
  - **TASK** (Austin, Debora, Phil): Also add guidelines for forks
- User issue [proposal](https://github.com/dhis2/notes/discussions/260) created by Birk
  - Some feedback but seems general consensus so far
  - Why do we need a user email?
    - Contact for app submission + future 
    - Organization email might be sufficient
    - User email may be needed for accounty things, so let's keep it for now.
    - **DECISION**: Keep user email, make Org email required, make App email optional
- Set up Amazon SES
  - What email address should send notifications?  noreply or apphub
  - Set up a app hub contact
  - **TASK** (Birk, Phil): Propose infrastructure solution for email notifications
- Created [Jira issue](https://jira.dhis2.org/browse/HUB-109) for enforcement of manifest fields by App Hub
- Created "MVP" version [proposal](https://github.com/dhis2/notes/discussions/268) for uploading all core apps
  - For step 2 - need to support "empty app" creation (no versions uploaded) to generate a new app id
    - Need to support "empty app" in v1 api too, since we will also want to enforce manifest ID == app hub ID in all cases
    - Should be easy to implement in creation API, need to consider how this affects the "read" APIs (i.e. apps disappear when last version is deleted)
    - **TASK** (Birk): Investigate support for empty apps
  - **DECISION**: Go for the cleanest, least hacky solution - wait until we have a holistic versioning strategy (so we also need to really push for that!)
    - **TASK** (Austin): Draft versioning and release management strategy proposal, review with **Viktor, Phil**
