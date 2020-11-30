**Date**: 2020-11-25

**Attending**: Jan-Gerke, Joe, Birk, Jennifer, Joakim, Ismay, Christos,
Austin, Martin, Edoardo, Hendrik, Bjørn

**Next Meeting**: Wednesday 9 December, 2020 @ 15:00

## Agenda

- General updates:
  - Standardize Github repo settings
  - UI Icons progress, [minutes from meeting Nov 24 available](https://github.com/dhis2/notes/pull/179)
- Updates from active working groups
  - Ports to App Platform
     - Add ports to: https://jira.dhis2.org/browse/DHIS2-10026
  - Feature toggling
  - Cypress
  - PWA
  - Plugin builds
- Merge strategies and workflows
  - https://github.com/dhis2/notes/issues/72
  - [Proposal](https://github.com/dhis2/notes/issues/72#issuecomment-733598206) to leave all merge strategies available in the Github interface for our repositories as we need them in different scenarios:
    - **Merge** when merging between the production and development branches.
    - **Squash and merge** when merging a feature branch to development or production branches.
    - **Rebase and merge** when merging a feature branch to development or production branches, and the feature branch contains work that should stay as distinct commits.
  - We use `semantic-release` to automatically release code, and their workflow recipes are well-proven so we don't need to invent our own: https://github.com/semantic-release/semantic-release/tree/master/docs/recipes#release-workflow

## Links

-   https://github.blog/changelog/2020-07-06-github-actions-manual-triggers-with-workflow_dispatch/
-   https://jira.dhis2.org/browse/DHIS2-8710

## Notes

-	How do we track full ports beyond step 3?

-   Can we do it automatically?

-   Cypress: we merged enabling automatic registering of commands, no
    need to call "registerCommands" in support/index.js

-   Cypress: also added a setup function that can be called, and it will
    automatically log in before each test, no need to do it manually.

-   Cypress: Will update to cypress 6 soon

-   Cypress: network shim is in progress, working on supporting testing
    against multiple versions, and non-deterministic responses when
    calling the same resource multiple times with different responses,
    progress on fixtures returning properly, and integration to the
    testing library.

    Need to figure out how to stop the request from propagating to the
    server, and need a way to test the full setup.

-   PWA: Progressing, fairly straightfoward to do service workers for
    static assets, we should probably do that for all apps now.

    Dynamic caching of API responses is more involved, esp. when
    considering partial caching for "some" resources.

-   Plugin builds: Related to caching and PWA work and push analytics.

-   Merge strategy proposal is accepted
    (https://github.com/dhis2/notes/issues/72#issuecomment-733598206).

-   Idea for rewriting applications, for some period of time we have
    duplicate applications.

    If we rewrite maintenance app, how do we link between maintenance
    app implementations if a user has a need to "drop to the classic"?

    We had a proof-of-concept for this a while back in the
    github.com/dhis2/mar-y repo.
