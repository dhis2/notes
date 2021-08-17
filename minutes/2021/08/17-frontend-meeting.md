# Agenda

- General updates
  - Welcome back, everyone ! 
  - Workflow templates have been updated:
    - Preview PRs available for all PRs without the "label" requirement
    - `cancel-in-progress` has been removed to allow release jobs to happen in sequence
  - The `d2-utils release` command has been ported to a GitHub Action.
    - [Testing progress tracked in PR](https://github.com/dhis2/workflows/pull/19)
  - Usage analytics is the first candidate for rolling out continuous delivery to the AppHub
    - Workflow for developers and QA has changed
    - PRs need to be tested and approved by **1 dev + 1 qa** before merging since merging to `master` means releasing a new version and publishing it to the AppHub
    - Starting as simple as possible and allowing the teams to adjust a bit before rolling out to more apps.

- Work group updates
  - PWA
  - Client-side caching
  - Developer Advocacy
  - Visual regression testing
  - i18n
  - Browserslist

- Other
  - ?

# Notes

## Work group updates

-   PWA:

    -   Published alpha version a month or so ago with PWA features
    -   Can be used with the @alpha platform dist-tag, and the @pwa
        dist-tag in runtime.
    -   Starting work on the headerbar update to add online status
        indicator
    -   Merging useOnlineStatus hook to master early
    -   Testing the dashboard app with the alpha version

-   Client-side caching

    -   Merged to app-runtime @beta
    -   Need to discuss necessity of cutting this as a breaking change with @ismay

-   Developer Advocacy

    -   Austin will follow-up the webinars and seminars.
    -   Looking for someone to step in and help out

-   Visual regression testing

    -   Focus on client-side caching
    -   No sponsorship from Chromatic, no response yet from Percy

-   i18n

    -   Mathieu leading a translation initiative across DHIS2, affecting
        the entire chain, including the software development side.

    -   Survey posted in the annual conference has some answers, needs
        to be clean up before sharing.

-   Browserslist

    -   `cli-style` should use the shared configuration:

        -   https://github.com/dhis2/app-platform/tree/feat-dynamic-modules/configs/browserlist
        -   https://github.com/dhis2/app-platform/blob/feat-dynamic-modules/.browserslistrc#L1

    -   All apps should update to reference it.

## Other

-   Upgrades to the d2-utils-docsite tool to give better API docs for
    React components.

