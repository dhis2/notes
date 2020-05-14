**Date**: 2020-05-13

**Attending (16)**: Austin, Birk, Bjørn, Christos, Edoardo, Erik, Hendrik, Ismay, Jan, Jan-Gerke, Jennifer, Joakim, Joe, Martin, Milagros, Wahed

## Goals
- Make everyone aware of the cross-team initiatives below
- Flesh out any potential complications or holes in these plans
- Set SMART milestone goals with specific timelines for each initiative
- Solicit volunteers to work on each taskforce (so think about what interests you!)

## Agenda

1. Present roadmap overview & solicit feedback
2. Establish taskforces
3. Set milestone targets

## Links

(DHIS2 account required)

* [2.35 Priorities Presentation](https://docs.google.com/presentation/d/1eDTeEFZNrzP2AwYqguVjA6QipSA354a8WaVHPOGvVw0/edit)
* [Meeting Recording](https://drive.google.com/file/d/1fjzVug8cTiVZzGqi4BMyU0pOhQ0PUZRX/view)

# Notes

## Initiatives
As we ramp up for 2.35 development, there are 4 major cross-team initiatives that we need to discuss and plan:

- [**Independent application releases**](https://jira.dhis2.org/browse/TECH-179) - this is critical to get into the 2.35 core so that we can begin to release applications.  Some sub-tasks:
    - Application CI deployment to App Hub
    - [Secure core application distribution](https://jira.dhis2.org/browse/TECH-370)
    - General, robust [server version toggling](https://github.com/dhis2/app-platform/issues/381) in apps
    - [Application metadata overhaul](https://github.com/dhis2/app-platform/issues/379)
    - Cross-team QA & Release coordination needed
- [**Platform PWA / Offline support**](https://github.com/dhis2/app-platform/issues/376) - [Dashboard PWA](https://jira.dhis2.org/browse/DHIS2-8341) is a high-priority deliverable by end-of-year, and is also critical for the Capture application (which already has some caching capability).  Both will involve some critical architecture for general-purpose offline support in the platform.  This includes [level 3 data caching](https://github.com/dhis2/app-platform/issues/372).  There are four components to this:
  - Enable a Service Worker and Web Application Manifest to "activate" PWA
  - Pre-load the selected data (certain dashboards, for instance) and save it in a persistent store (localstorage / indexeddb / websql) for later recall (related to #372)
  - Implement UI changes for “offline mode” - disable links to online-only apps, support an online/offline toggle, disable online-only features
  - Update application CSS and functional UI to support small-form-factor devices (phones and tablets)
- [**Platform improvements & adoption**](https://github.com/dhis2/app-platform/issues?q=is%3Aopen+is%3Aissue+label%3Aroadmap) - There are several cross-cutting improvements to the platform that could have huge benefits to the DHIS2 product as a whole as well as our development workflows.  The highest priorities of these are, in order of importance:
  - [i18n overhaul](https://github.com/dhis2/app-platform/issues/369)
  - [plugin builds](https://github.com/dhis2/app-platform/issues/375)
  - Platform coverage - target >= 50% of core apps by 2.35
  - [Data caching levels 1 and 2](https://github.com/dhis2/app-platform/issues/372)
  - [bundle size and performance](https://docs.google.com/presentation/d/1eDTeEFZNrzP2AwYqguVjA6QipSA354a8WaVHPOGvVw0/edit#slide=id.g76d7b97cfd_0_0)
  - [Functional end-to-end testing & automation](https://github.com/dhis2/cli-utils-cypress)
  - [Full-coverage UI Components](https://github.com/dhis2/ui) - particularly ported `d2-ui` components
- **Developer evangelism & app development academy** - We had to cancel the planned DHIS2 developer academy (with 30 registered participants) in Kigali, Rwanda because of COVID-19.  Instead, we'll be hosting a live online academy in June and creating some independent learning material for a self-paced course.  I'd really like to foster a more connected community through these efforts, so that each third-party app developer isn't working in a silo.  These efforts also serve a dual purpose as they help us to improve our tools, create really robust documentation, and facilitate new core developer onboarding.
  - Centralize developer documentation at [developers.dhis2.org](https://developers.dhis2.org) 
  - Write some basic tutorials and guides
  - Help facilitate the live academy
  - Help build and support the external developer community
  - Feedback & contribution processes for platform libraries

## Taskforces

* Continuous Application Delivery
    * Austin(*)
    * Erik
    * Birk
    * Hendrik (Feature Toggling)
* PWA & Dashboards
    * Jan
    * Edoardo
    * Jan-Gherke (app-runtime data caching)
    * Joakim (tracker perspective & advice)
    * Joe (UI/UX)
* Platform Improvements & Adoption
    * Ismay
    * Jennifer (i18n)
    * Martin (i18n)
    * Jan-Gherke (e2e testing & automation)
    * Bjørn (plugins & bundle size)
    * Hendrik (UI)
* Evangelism & Documentation
    * Christos
    * Milagros
    * Wahed (coordinate w/ Magnus @ UiO)
    * Hendrik (user/market research)
    * Jan-Gherke

(*) Austin will help to coordinate and contribute to other taskforces as well

## Next Steps

1. Austin will set up first meeting or slack channel for each group
2. Each taskforce decides on priorities and component parts for 2.35
3. Austin to propose a documentation format, location, and process for "taskforce knowledge" & contribution docs
4. Each taskforce presents priorities, ongoing work, and open questions at meeting in 2 weeks

**Next Frontend Initiatives Meeting**: Wednesday, May 27, 2020
