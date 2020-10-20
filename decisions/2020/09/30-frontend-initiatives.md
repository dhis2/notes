**Date**: 2020-09-30

**Attending (Speaking)**: Jan Henrik, Austin, Joe, Ismay, Hendrik,
Christos, Joakim, ..

**Next Meeting**: Wednesday, October 14 @ 15:00 CET

## Agenda

1.  Platform initiatives before 2.36 prioritization
    -   Library release process
    -   Port all/most app to latest platform to step 3 (progressive
        modernization)
    -   Implement Key App Platform Features
        -   Server version toggling
        -   State management
        -   Plugin builds
    -   CI App Hub Publication
    -   App testing & reduced tech debt

## Links

(DHIS2 account required)

* [Agenda](https://github.com/dhis2/notes/issues/126)
* [Meeting Recording](https://drive.google.com/file/d/18Y2AGfK0ZTKrcgjD1_RxnkW-Yj734pjA/view)
* [Tech Debt Topics](https://docs.google.com/document/d/1q_LDIZcaoGbKQ-gz1SfOJ3Fy-SeYmCn5e7n3GSCTK5Q)

## Progressive modernization

Each app can be progressively modernized using the following procedure:

1.  (if non-React) rewrite in React
2.  Migrate to App Platform, using `app-runtime-adapter-d2` to support
    existing `d2` usage
3.  Update name, version, and publish config for automated releases to
    App Hub
4.  Upgrade components to `ui` from `material-ui` and `d2-ui`, improving
    `ui` widgets if missing support
5.  Replace imperative data access (`fetch`, `engine.query`)
    with declarative data dependencies (`useDataQuery`) as close
    as possible to the components using the data
6.  Remove `app-runtime-adapter-d2`
7.  [Replace Redux or other state management with standardized state management solution (or remove app-level state)](https://github.com/dhis2/app-runtime/issues/444#issuecomment-622323029)
8.  Replace Router with [App Runtime router](https://github.com/dhis2/app-platform/issues/374) (when it exists)

## Notes

### Library contributions

Context: https://github.com/dhis2/notes/issues/125

We are still struggling with all the frontend teams contributing to
shared code libraries, e.g. UI.

Suggestion to allocate time to introduce everyone to e.g. UI.

Introduction meeting, recorded presentation, documentation, internal
"course" for all our libraries would be helpful.

This is not intended to solve the prioritization of work, but rather
help get everyone up to speed and a good first step to contribute to
shared libraries.

### JIRA and GitHub

Arguments for GitHub is:

-   that it is closer to the code and requires less setup for new code
    units.
    
-   More straightforward for external developers.

Arguments against GitHub:

-   Maintaining two flows for the same thing is suboptimal.

-   We have tasks that fall in the cracks due to having two systems.

-   Need special automation, and or special rules to handle the added
    complexity.

-   It is probable that we cannot completely replace JIRA for apps and
    libs and go all in on GitHub.

### Propagation of libraries

When a library is released, we want to propagate that change to all the
other apps and libs that depends on it to make sure that everything uses
the latest code.

This requires some automation and some setup in our repos.

### Port as many apps as we can to the App Platform

See the progressive modernization list above.

The goal is to get as many apps through step 3 as we can:

> 1.  (if non-React) rewrite in React
> 2.  Migrate to App Platform, using `app-runtime-adapter-d2` to support
>     existing `d2` usage
> 3.  Update name, version, and publish config for automated releases to
>     App Hub

### Server version toggling

Needed to get movement on the feature toggling applications.

We need to use _versioned_ API versions, because end-points
are redirected to either to the newest version, or to a specific
version of the API that may be different from the version of DHIS2 which
is running.

### State management

We should think about a standard approach, but this is not high priority
right now.

### Plugin builds

Moving from NPM distributed plugins to a plugin that is bundled with the
application, so the App Platform needs to be able to build plugins.

### Publish to App Hub

CI to App Hub to a staging channel, basically `d2-app-scripts publish`
in addition to `d2-app-scripts deploy`.

### App testing and reducing tech tebt

Need to update the document to understand what technical debt we have.

Will be discussed in the next meeting.
