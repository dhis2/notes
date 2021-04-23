**Date**: 2020-11-11

**Attending**: Hendrik, Joakim, Christos, Austin, Jan, Jan-Gerke, Joe,
Viktor, Birk, Edoardo, Martin, .. ?

**Next Meeting**: Wednesday 25 November, 2020 @ 15:00

## Agenda


-   Quick general updates:
-   Migration to JIRA is progressing.
-   There was a Cypress meeting yesterday and [the minutes are available](https://github.com/dhis2/notes/pull/140), feel free to
    comment even if you weren't in the meeting.
-   Updates from active working groups
-   [Prioritization for ui issues](https://github.com/dhis2/notes/issues/125)
    -   The proposal is to handle prioritization of library issues as
        part of the main prioritization process in JIRA. This allows
        better visibility across app and library dependencies, better
        visibility for the project about what work is done, etc.
-   Migrating d2-ui components
-   Tech debt review

## Links

(DHIS2 account required)

*   [Agenda](https://github.com/dhis2/notes/issues/155)
*   [Platform Plugin Architecture](https://docs.google.com/document/d/18Qix9cfWlyrXVgkaS2K-IKHQzcbIGWDlxD5GIoIWa7I/edit)
*   [Tech Debt Topics](https://docs.google.com/document/d/1q_LDIZcaoGbKQ-gz1SfOJ3Fy-SeYmCn5e7n3GSCTK5Q/edit)

## Notes

### Working groups

-   Cypress: testing is progressing.
-   Cypress: Add documentation for the cli-utils-cypress.
-   Cypress: Working on a Network Shim plugin for Cypress.
-   PWA: Progress on specifically the Dashboards PWA.
-   Platform: Alert Service coming soon.
-   Platform: Plugin builds, how to add plugin builds to the platform.
-   Feature toggling: Collecting use cases in [this Notes issue](https://github.com/dhis2/notes/issues/138)

### Prioritization of library issues

-   We are going to handle prioritization of library issues as part of
    the main prioritization process in JIRA. This allows better
    visibility across app and library dependencies, better visibility
    for the project about what work is done, etc.

-   There is a question of visibility of issues in JIRA since a user
    account is required, how do we reach externals developers, make it
    searchable, etc.?

### Migrating d2-ui components

-   Need to document UI design goals.
-   We have a lot of d2-ui components that need to be rewritten in UI.
-   Sharing dialog is in progress, [PR](https://github.com/dhis2/ui/pull/24).
-   What do we test with Jest, and what do we test with Cypress.
-   Cypress for high complexity tests, Jest for low complexity.
-     [Layouts POC](https://github.com/dhis2/ui/pull/27) was drafted a while ago but has gotten stale, need another pass.  This replaces [d2-ui-core layouts](https://github.com/dhis2/d2-ui/tree/master/packages/core/src/layout)
-    Edoardo is also working on implementing the [d2-ui-file-menu](https://github.com/dhis2/d2-ui/tree/master/packages/file-menu) with UI components in [analytics](https://github.com/dhis2/analytics/pull/655)

### Tech Debt Review

Some thoughts of what tech debt means to some of us:

-   Structural or implementation complexity that doesn't have a
    manifestation in the user facing experience of the app.

-   Tech Debt: 'Required' stuff vs. 'Nice to have' stuff.

-   Anything that needs to be done, but doesn't show up in JIRA.

**CTA**: Please look through the [Tech Debt Topics](https://docs.google.com/document/d/1q_LDIZcaoGbKQ-gz1SfOJ3Fy-SeYmCn5e7n3GSCTK5Q/edit) and add things you are
aware of.
