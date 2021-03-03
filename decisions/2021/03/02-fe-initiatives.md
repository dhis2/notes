Date: 2021-03-02

Attending: Austin, Birk, Bjørn, Christos, Debora, Edoardo, Ismay, Jan
Hendrik, Jan-Gerke, Jennifer, Joakim, Joe, Martin, Médi-Rémi, Milagros,
Viktor

## Notes

### Dynamic modules

Coming along nicely, based on SystemJS. Demo-time if there is time!

### GitHub Actions stuck in "queued"

GitHub needs to manually move our workflow runs that are stuck in a
queued phase to a completed phase. Then we can re-run them and get
the 2.35.2 release built.

### Working group updates

#### Developer portal

Revamped developer portal is live!

All content has been ported over.

Will start adding new content now.

One-stop-shop for DHIS2 developer needs, more guides and tutorials are
coming.

Added the core developers with access rights to the
dhis2/developer-portal repo.

#### Cypress

Add network shim to an existing app, didn't work perfectly.

Network shim doesn't support static fixtures defined manually, needs to
be fixed in the shim, and is being worked on.

#### UI & Platform

Tree-shakable library builds are now available. Now we only transpile
our sources, which makes it easier to tree-shake in the application.

In UI we've run into some problems related to imports in Storybook.

#### App Hub and App Management updates

App Hub taken a bit of a backseat to 2.36 fixes.

Some deployment issues on AWS EBS.

App Management changes relate to the ability to publish to the App Hub
from our development pipelines, so we can leverage the bundled app
override mechanisms. 

Faster deployments to the field.

### Topics

#### PR previews

Using a GitHub Action to build and publish a built artifact to Netlify.

The artifact is then pushed to Netlify and added to the PR as a
deployment.

[Surge](https://surge.sh) is an alternative to [Netlify](https://netlify.com) when it comes to PR previews.

Next steps:
- @paschalidi will put together a short document comparing Surge, Netlfiy, and [Vercel (formerly Zeit Now)](https://vercel.com/)
- We need to set up debug.dhis2.org-only CORS configuration (@Philip-Larsen-Donnelly)
- @varl is taking a look at the actions in Christos' demo repo
- Once we have a reproducible workflow, we can just copy it to our app repos!

#### When will we be able to deploy independent applications on App Hub?

Soon(tm)!

2.36 will have significant improvements to the App Management, App Hub
and the developer workflows.

#### a11y updates

When writing integration tests for the Scheduler app using [cypress testing library](https://testing-library.com/docs/cypress-testing-library/intro/), which forces
use of accessible selectors, this triggered a lot of changes to UI components.

Base a11y target, there is a proposal for it:
https://github.com/dhis2/notes/discussions/238

Needs a decision to be reached on it.

First we look at the components in UI and fix the obvious missing parts,
and consider application a11y separately, e.g. how to get from the
headerbar to the "main" application.

#### Feedback on the support rotation

Feel free to join the rotation!

To see who is on rotation: https://calendar.google.com/calendar/embed?src=c_aebpolkmfvanjcfgf8f96bnbi8%40group.calendar.google.com&ctz=Europe%2FOslo

#### Anything else?

##### Gather town

There's a DHIS2 Virtual Office -- enlist now!

##### Dynamic modules demo

Chunking and shared chunks of libraries.

Implemented using SystemJS.

Generate production and development import maps.

Very good support for source maps, also locally.

Fair reduction of size over the wire.

Better caching of shared resources.

Working on integration into the app platform build scripts, it's there
but needs some polish before prime time.
