**Date**: 2020-12-09

**Attending**: Birk, Bjørn, Christos, Hendrik, Ismay, Joe, Martin,
Viktor, Jennifer, Jan Henrik, Joakim, Edoardo, Milagros, Jan-Gerke

**Next Meeting**: January 6, 2020 @ 15:00

## Agenda

_When_: December 9, 2020 @ 15:00 CET
_Where_ : Remote

# Agenda

-   General updates:

    -   GitHub Discussions in the Notes repo!
    -   Auto-merging coming soon in GitHub (https://github.com/dhis2/notes/issues/71)
    -   Updates from active working groups
    -   Ports to App Platform
    -   Feature toggling
    -   Cypress
    -   PWA
    -   Plugin builds

-   Migration to Yarn2 (experimental)

## Notes

### Working group updates

-   Port to application platform

    -   Maps app blocked by plugins

-   Feature toggling

    -   No updates since last time

-   Cypress

    -   Install command is improved, has been modified to be more
        flexible and allow to install gradual changes and adding new
        functionality.

    -   Implementing a codemod for updating all the get/find calls that
        use the special selector syntax.
    
    -   Network shim, add some tests and refactor slightly, there is a
        PR up and would be good to get in soon. Mostly good to go.

    -   `enableAutoLogin` functionality in cli-utils-cypress@4,
        automatically registers the "must haves", and supplies helper
        functions that are manually registered.

-   PWA

    -   Figuring out what to show/hide in mobile view, mostly done.

    -   Implementation side is in progress.

    -   Changes to components needs to be coordinated with UX so we get
        mobile variants.

    -   Platform side support for static asset caching, service workers.

    -   Working on dynamic caching for the Dashboard by recording the
        network requests into an encrypted indexDB.

    -   Static analysis in the long term for what data dependencies a
        plugin has.

-   Plugin builds

    -   Related to PWA in a lot of ways, in addition to push analytics
        (generating visualizations on the server).

    -   Currently 3 different systems, need to consolidate to one.

    -   Sharing dependencies between the host and the embedded plugins will come later, but will be considered in the initial design.

### Yarn2 migration

-   Current the Yarn2 implementation is self-contained in the platform,
    so users can use Yarn1 or NPM to build their applications.

-   Move the app platform to use Yarn2

-   Draft PR in https://github.com/dhis2/app-platform/pull/491

-   Exhaustive list of benefits in the PR.

-   Yarn2 has "portal" dependencies, which will make shelling an
    application a lot more stable.

-   We must have proper dependencies declared in our libraries and
    applications. The current implicit resolution behavior will _not_
    work.

-   It is possible to apply patches to dependencies through Yarn2 if
    they need to be modified.

-   We can use `resolutions` in the Shell to enforce our built-in
    versions, we need to throw warnings when doing so.

-   Way forward is to merge to alpha or next and play around with it for
    a bit.

### Icon design guidelines

-   Icon design guidelines are available in:
    https://github.com/dhis2/design-system/pull/31

-   There is a request process for new icons (or ping UX on Slack).

-   UX will happily assist on migrating away from MUI icons.

-   The request process will involve determining if the icon should
    live in the app or in the icons library.
