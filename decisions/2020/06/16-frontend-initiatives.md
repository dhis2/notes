**Date**: 2020-06-16

**Attending (16)**: Austin, Birk, Bjørn, Christos, Edoardo, Erik, Hendrik, Ismay, Jan, Jan-Gerke, Jennifer, Joakim, Joe, Martin, Milagros, Wahed

**Next Meeting**: Wednesday, June 24 @ 15:00 CET

## Agenda

- Initiative progress & priorities
  - [**Top Priority** - Continuous Delivery](https://github.com/dhis2/notes/issues/114)
  - Webinars and Workshops
  - Platform coverage
  - [data caching](https://github.com/dhis2/app-platform/issues/372)
  - [plugin builds](https://github.com/dhis2/app-platform/issues/375)
  - [PWA](https://github.com/dhis2/app-platform/issues/376)
- Discussions & Decisions
  - [Dependency Resolution approaches](https://github.com/dhis2/notes/issues/67)
  - ui5 successes & challenges + [major release strategy](https://github.com/dhis2/notes/issues/101)
  - How can we better push initiatives forward?

## Links

(DHIS2 account required)

* [Meeting Recording](https://drive.google.com/file/d/1C0ysMCQaV-ix-j0Hk04bEDwDhXpuiYpi/view)

# Notes

### Continuous Delivery

Top priority, led by Birk, Austin, Erik - to work with backend team to complete "application lifecycle" (meeting Monday)

For all frontend devs:

- Think about how decoupled releases will affect planning and app development workflows
- Consider benefits and challenges of implementing feature toggling and elimination of backporting in core apps

### Webinars & Workshops

Facilitator team:

- Jan-Gerke
- Christos
- Hendrik
- Wahed
- Milagros (Americas time zone)

### Platform Coverage

Clarification : this means the percentage of our applications which are built on the Platform!

Issues aren't fully **done** until they've been propagated to all apps.  For example, implementing a fix in the Headerbar in `ui-widgets` 

Moving apps to the app platform can be be surprisingly straightforward, sometimes easier than trying to upgrade components in "legacy" apps

The platform goal is to reduce our maintenance burden across all our ~35 apps.

Hendrik converted two apps in an afternoon (!)

Goal: systematically go through our apps and upgrade them to the platform

### Platform features

- **Feature Toggling**
  - Goal is to coalesce to a **single release stream** for 
- **Data Caching**
  - Austin to put together initial implementation for level 1 and level 2 caching
  - Work with Ismay (scheduler-app) and Jan-gerke (OU Tree) to test implementations
- **Plugin Builds** 
  - Coming soon as well
  - Austin to write and share spec
  - one option - native `<script type="module">` in-browser module loading
- **Progressive Web Apps (Dashboard)**
  - @jan worried about timeframe for 2.35
  - If we get continuous delivery into 2.35, we can push this deadling to December / January, which is one reason continuous delivery is top-priority
  - To set up meeting for 

## Discussions and Decisions

These will open for discussion from later this week, with 

### Wrapping and Re-exporting Dependencies

Two separate issues

1. Re-exported external dependencies (`final-form`, `react-final-form`, `prop-types`)
2. Singletons in DHIS2 apps (`react`, `react-dom`, `styled-jsx`, `@dhis2/app-runtime`, `@dhis2/d2-i18n`, `@dhis2/ui-core`)



We should consider these as separate issues, and some of the main concerns are:

- We want to ensure we enable tree-shaking of re-exported library components
- Wrapped dependencies can lead to duplication and misconfigured 
- There is a non-trivial maintenance cost of duplicating dependencies across applications (since they're peerDeps of libraries
- Using peerDependencies expands the matrix of dependency combinations we need to support
- Yarn and npm don't have great support for de-duplication and don't guarantee hoisting of transitive dependencies (unfortunately, though we would like them)

**Next Steps** - Put together 2 proposals (@austin), open for discussion and feedback, address decision at next meeting

### Major Release Strategies

UI v5 post-mortem

- Release was too big (Too many things combined into one release)
- Alpha was maintained for too long



Going forward (proposal)

- Smaller releases, focused on one or two components with breaking changes
- Avoid breaking changes unless strictly necessary, since we have more and more consumers
- More people  with consumers **before** cutting a major release (work with other core teams in alpha phase)
- **A release shouldn't be considered "complete" until it's been propagated to all core apps**
- **We are all one team and should contribute to the cross-product libraries like UI (even if just reviewing code)**

**Next Steps** - Austin to formalize actionable proposal in Release Stategy issue for ratification next week

### Pushing initiatives forward

*Deferred* - to discuss next week
