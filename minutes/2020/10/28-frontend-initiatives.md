**Date**: 2020-10-28

**Attending (11)**: Austin, Viktor, Birk, Christos, Edoardo, Hendrik,
Jan Henrik,  Jan-Gerke, Joe, Martin, Milagros, Wahed

**Next Meeting**: Wednesday 11 November, 2020 @ 15:00

## Agenda

-   Quick general updates:

    -   New unified GitHub workflows for [apps](https://github.com/dhis2/workflows/blob/master/ci/dhis2-verify-app.yml), [libs](https://github.com/dhis2/workflows/blob/master/ci/dhis2-verify-lib.yml), [node](https://github.com/dhis2/workflows/blob/master/ci/dhis2-verify-node.yml)

    -   Work started on practical plans on GitHub to JIRA migration (#135)

-   Updates from active working groups

-   New working group for Feature toggling

    -   All teams do an initial check on "known" features to toggle
    -   Working group extracts use cases and works on a proof-of-concept
    -   Pilot integration into chosen apps

-   Cypress and Gherkhin - next steps for decision

-   Migrating d2-ui components

-   Tech debt review

## Links

(DHIS2 account required)

*   [Agenda](https://github.com/dhis2/notes/issues/134)

## Notes

### General updates

Let Viktor know if you are having issues with the unified workflows.

### Working groups

Four working groups in May:

*   _Independent app releases_: good progress

*   _PWA offline support_: put off to after 2.35

*   _Platform improvements_: main one with progress, converted several apps to
    the platform, progressive modernization working well, moving away from d2

    Some challenges related to d2, and replacing d2-ui components, gradual
    migration may be possible with the d2 runtime adapter. Hard to replace when
    using the d2 models.

    There is good progress on testing and test automation, more people
    are getting involved.

    There is some movement on porting d2-ui components to UI.

    Plugin builds initiative restart, to enable a move from mono to
    single repo with multiple outputs.

    i18n, caching, and performance: work has started.

*   _Developer evangelism_: academy in August. Went well, some wrap up and clean
    up to do before the new one coming in early 2021.

    Looking at a hiring for a developer advocate position

### Feature toggling working group

_Leads_: Austin, Hendrik, Christos

Others are welcome to contribute, Austin and Hendrik may reach out an ask teams
for specific details or units of work.

### Cypress and Gherkin

Points from discussion:

-   The abstraction of Feature files can be nice.

-   Maybe not everything needs to be a Feature file.

-   Can we use feature files for some things and not others?

-   A limited number of acceptance tests based on feature files, and the rest in vanilla?

-   What is the actual overhead of Cucumber?

-   Push test results to Zephyr.

-   All in on vanilla Cypress? All in on Cucumber Cypress? Is a hybrid approach viable?

Next steps:

-   Keep going as we are for 2 months.
-   Gather information and use cases we run into.
-   Integrate our test reports into Zephyr (with and without Cucumber).
-   Refer to [#136](https://github.com/dhis2/notes/issues/136).
    
### Migrating d2-ui components, Tech debt review

We didn't get to these today.
