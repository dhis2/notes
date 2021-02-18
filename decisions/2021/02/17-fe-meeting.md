Date: 2021-02-17

Attending: Austin, Birk, Bjørn, Christos, Debora, Edoardo, Hendrik, Ismay, Jan Henrik, Jan-Gerke, Joakim, Joe, Kai, Martin, Médi-Remi, Milagros

Next Meeting: Tuesday, March 2, 2021 @ 15:00

## Agenda

### Updates
- General
- Working groups

### Topics
- Add network shim to apps that already use cypress (utils?) so we can run tests on GH (@Mohammer5)
- Start a discussion about component accessibility in @dhis2/ui (@paschalidi)
- PR previews short demo on the solution (@paschalidi)
- styled-jsx bug in ~3.4.x~ 3.3.3 (not yet fixed in 3.4.x)

### Questions
- When will we be able to deploy independently applications? @paschalidi

## Notes


* Cypress
    * Want to deprecate - getWithDataTest / findWithDataTest
    * Use helpers instead of commands
    * Need to document
* PWA/Offline/Responsive
    * PWA deferred to after 2.36
        * Beta on App Hub in Q1 2021
    * Responsive Working on control bar + portrait / tablet
* UI + Platform
    * We want to upgrade shell to ui v6
    * Less of an issue in dynamic module world
    * PR in progress to replace context layering with DOM stacking
    * Coming soon - tree shakable UI and other libraries
    * Want to add bundle size CI checks
    * UI Storybook
        * Awesome new layout and design and features!
        * Next steps:
            * Review implementation with Platform team
            * Present to wider audience including masters students
            * Document how to write and read docs
        * Suggestion: overview / cheatsheet page
        * Undecided what the future intersection of ui docs and design system will be
* Developer Outreach & Resources
    * New slack workspace (yay!)
    * Next step: organize a meetup / webinar
    * Developer portal in progress

* Cypress Network Shim
    * Runs in plugin, should be very fast
    * Want to run on GH Actions CI, starting with SMS Config App after 2.36
    * Need to determine if there’s a detrimental impact on org-wide parallel job limit
    * Hendrik demo’d how to use the shim (more in-depth demo later)
    * Need to document and write introductory tutorial
* Accessibility
    * Nice new tools in storybook plugin
    * Need to align on what level of accessibility we want
    * Issue - MenuItems not tab-able
    * Need some user feedback on what they actually want
        * Will get some feedback from community when replacing MUI with @dhis2/ui
        * For example - can’t use esc in menu
        * Might get some pushback from community, will need to implement that feedback
        * Should test keyboard after migration to ui
    * “Usability” - Agree that keyboard usability is baseline that we want
    *  “accessibility” - don’t stop the browser from doing what it wants to do
* PR Previews - to discuss next week
* When will we be able to independently deploy applications? - to discuss next week
* Styled JSX - there is [a bug in 3.3.3 (not yet fixed in 3.4.x)](https://github.com/vercel/styled-jsx/issues/695) which affects the `styled-jsx/babel` plugin.  This might might bite you, be aware - @austin will pin the version in @dhis2/cli-app-scripts to 3.3.2 to hopefully avoid this in most cases
