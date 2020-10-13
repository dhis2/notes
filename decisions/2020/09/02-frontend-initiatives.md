**Date**: 2020-09-02

**Attending (speaking)**: Austin, Jan-Gerke, Martin, Joe, Jan Henrik,
Ismay, Birk, Erik, Hendrik, Christos, Edoardo, Jennifer, ..

**Next Meeting**: September 30, 2020 @ 15:00 CET

## Agenda

-   Academy recap
-   Continuous app delivery - beyond 2.35
-   Feature toggling, App Platform coverage, and Dashboard PWA -
    initiatives coming soon
-   2.35 processes retrospective - everyone contribute 1 positive and 1
    negative!

## Links

(DHIS2 account required)

- [Meeting recording](https://drive.google.com/file/d/1NaEMZDPmzgQCUC_BuReAW4VTX2k3hWSs/view?pli=1).

## Notes

### Academy recap

Went well overall! Great job, everyone. Still working on grading, and
finishing up.

Looking at hiring another developer advocate to offload the team a bit
WRT developer outreach.

Valuable feedback, better at structuring our courses, identifying gaps
in our documentation, etc.

Building out the DHIS2 developer community is important to us, something
we will do more of.

### Continuous app delivery - beyond 2.35

We have continous app delivery capabilities in 2.35 (:tada:), we can
release a new version of an app and it can be installed "on top" of the
bundled app to replace it.

If the new version is uninstalled, the system falls back to the bundled
version again.

We need to reframe our thinking in terms of releases that are not tied
to DHIS2 Core versions.

Will help with testing since any development app can be run the same way
as we run apps in production.

`d2-app-scripts deploy` can deploy to a running instancing. We also want
`d2-app-scripts publish` to publish a new version to the App Hub to
enable continuous integration and delivery of apps.

### Feature toggling, App Platform coverage, Dashboard PWA

-   Feature toggling becomes more important with continuous releases, to
    support multiple versions of DHIS2 with the same version of an app. 
    _Working group_: Hendrik, Christos

-   App Platform coverage: "the number of apps that use the platform".
    Porting our apps to the Application Platform. Faciliate the
    propagation of changes of the platform itself; how are we going to
    automate updates of the platform? Leverage the App Platform as the
    Web Portal (Struts).
    _Working group_: Austin (with support from snipers)

-   Progressive Web Apps, back into focus. Dashboards PWA due before
    xmas. Platform pieces for caching and offline support.

-   Frontend platform pieces?

    -   Prefer Jest where possible over Cypress

    -   UI libraries, 60+ issues open, good to have a meeting and talk
        about those issues as the frontend and get collaboration going.

    -   Move d2-utils-cypress to a monorepo, more automated, easier to
        add tests, etc.

    -   Privacy and security considerations when caching (e.g.
        encryption). Session timeouts on the platform itself to hide
        sensitive data, e.g.

### 2.35 Process Retrospective

One positive and one negative thing, added to a Google Doc in
collaboration.

-   :heavy_plus_sign: Hooray for 5 new Analytics features.
-   :heavy_plus_sign: Push to get SMS Config App implemented and out in 2.35.
-   :heavy_plus_sign: Working together as a single frontend team, less silos.
-   :heavy_plus_sign: Academy went very well.
-   :heavy_plus_sign: Better communication and overview across teams,
    frontend and backend, great to see !
-   :heavy_plus_sign: Joe is a Super Hero. Someone clone this man !
-   :heavy_plus_sign: Everyone is happy to help.

-   :heavy_minus_sign: Backporting is a pain.
-   :heavy_minus_sign: Planning app rewrites including speccing and testing. 
-   :heavy_minus_sign: More realistic planning. Had to adjust things at
    the last minute.
-   :heavy_minus_sign: Detailed specs for all features, need more
    functional requirements to know what we are building and for the
    test team to know what they should test.
-   :heavy_minus_sign: Not sure about the best way to contribute to the
    UI library, need to be better at facilitating that.
-   :heavy_minus_sign: Last minute feature requests need to go into a
    more holistic planning.
-   :heavy_minus_sign: Roadmaps! For libs, platform, and apps.

