
# Agenda

-   General updates
  -     Hard freeze today
  -     App Platform 8.0.0 after hard freeze, notable changes:
    - app-runtime 3.x (https://jira.dhis2.org/browse/LIBS-200, [changelog](https://github.com/dhis2/app-runtime/blob/master/CHANGELOG.md#300-2021-09-07))
    - styled-jsx 4.x
    - jest 27.x
    - Proxy support for local development
    - behaviour change in AlertService
-   Working groups
  - PWA
  - Client-side caching
  - Developer Advocacy
  - Visual regression testing
  - i18n
  - Browserlist
-   Other

# Notes

-   PWA
    -   Due for prime time for Dashboards in 2.37.0
    -   Manifest.json bug fixed
-   Client-side caching 
    -   Included in app-runtime 3.x
    -   SWR is opt-out, there is a list of the breaking changes:
        https://github.com/dhis2/app-runtime/blob/master/CHANGELOG.md#breaking-changes
    -   Tested in all apps that use the Data Engine, and should be a
        smooth transition in most cases.
    -   Depends on app-platform 8.x
-   Developer Advocacy
    -   German has accepted an offer with us
-   Visual regression testing
    -   Demos are complete and can be tested
    -   Local snapshot testing solution could be a workaround
    -   Stalled on budget, will follow up again after 2.37.0
-   i18n
    -   There is a larger push for translations and localizations in
        DHIS2 that have requirements that impact our future i18n
        solution.
    -   Ongoing work with with the DHIS2 Localization Team.
    -   Tied into global shell, dynamic modules, translation hoisting
        from dependencies, interpolations, pluralizations, formatting,
        etc.
-   Browserslist
    -   Same status as last time, not yet extracted and published as a
        sharable configuration package.
    -   Configuration file monorepo.
-   Other
    -   Global shell
        -   Moving the shell to the top-level, so that shell can swap
            out the application dynamically.
        -   Think about it and we can discuss this more next time.
