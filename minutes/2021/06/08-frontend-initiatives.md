# Frontend Initiatives Meeting

**When**: June 08, 2021 15:00 CET **Who**: Austin, Birk, Bjørn, Debora,
Edoardo, Hendrik, Ismay, Jan-Gerke, Jennifer, Kai, Martin, Médi, Simona, Viktor

## Agenda

- General updates
  - Proposal for how [application
    versions](https://github.com/dhis2/notes/discussions/293) will be handled
    in the CI/CD world in progress
  - DataTable has been released in UI along with new features:
    https://github.com/dhis2/ui/blob/master/CHANGELOG.md
- Lighthouse testing on CI (see
  [slack](https://dhis2.slack.com/archives/C0BP0RABF/p1623050297078300)).
  - If everyone likes this we could add it to Jira.
- SameSite cookie changes in Chrome
- Work groups updates
  - Cypress
  - PWA
  - Developer Advocacy
  - Client-side caching
    - Outcome of the proposals:
      https://github.com/dhis2/notes/blob/master/minutes/2021/06/03-client-side-caching.md
  - PR Previews
    - New workflows available, can be [installed with
      `d2-style`](https://dhis2.slack.com/archives/C0BP0RABF/p1622810229070700) 
    - To do: updating the default CORS whitelist in databases and environments.
      - Done for debug.dhis2.org/dev
    - Example workflow:
      https://github.com/dhis2/workflows/blob/master/ci/dhis2-preview-pr.yml
  - Visual regression testing
  - i18n
  - Browserlist
- Misc?
- Lighthouse testing on CI (see slack). If everyone likes this we could add it
  to Jira.

## Notes

* General updates
  * Proposal for how application versions will be handled in the CI/CD world in
    progress
    * Related notes discussion: https://github.com/dhis2/notes/discussions/293
      * Upcoming changes: Read through them to be aware of upcoming changes and
      find potential issues so we can catch those early
    * Currently we don't care about app versions in the package.json, but we
      will in the future
    * PR contains details
    * Libraries won't get bumped, only applications
      * possible exceptions: d2 (& d2-ui)
  * DataTable has been released in UI along with new features:
    https://github.com/dhis2/ui/blob/master/CHANGELOG.md
    * Other features: Modal can be hidden now with stateful contents
    * Max-width prop for tag component
    * AlertBar has a hide prop as well
* Lighthouse testing on CI (see
  [slack](https://dhis2.slack.com/archives/C0BP0RABF/p1623050297078300)).
  * If everyone likes this we could add it to Jira.
  * Run tests automatically
  * Has to be run on every commit on master to be able to rely on it
    * Could be combined with the PR preview label or with static files
  * [Jira issue](https://jira.dhis2.org/browse/DEVOPS-61)
* SameSite cookie changes in Chrome
  * Temporary solution exists using chrome flags until version 94
  * Chrome Version 94 will remove that feature and replace it with token based
    auth
  * Jira issue: https://jira.dhis2.org/browse/DHIS2-11311 
  * Alternative:
    * Use a local instance (running it on the localhost or have them on the
      same machine)
    * Maybe a local proxy, would have to be built into the dhis2 dev
      environment
      * Potential issues with absolute urls that are followed
  * Long term solution: OAuth server
- Work groups updates
  * Cypress
    * Network shim
      * implemented in scheduler app and works on CI
      * currently on alpha, will go into master soon
    * Upcoming breaking change
      * drops the `run` & `open` commands
      * to make it work the same way on CI and other environments
      * eliminates the need for npx
      * is being aligned with the shared helpers inside the cli helpers engine
    * Workflows from workflows repo can be used soon, docs are still missing
      before it can be released
      * Will be released either by the end of this or the start of next week,
        probably!
  * PWA
    * New self-destruct mode that will clean up rogue service workers to
      replace older service workers
      * Details will be covered during the meeting on the 9th June '21
        (PWA/caching API meet)
      * Rogue service workers will cause users to see old version of app even
        when it's been rebuilt recently.
      * When updating a CRA app to a platform app, the service worker doesn't
        get updated, which caused the service worker to be rogue (prior to the
        self-destruct change)
    * Prototype code is being put into the app-runtime right now and will be
      merged into the alpha version soon
    * registration process needs to be made rock solid & performance
      improvements needs to be implemented to complete the current iteration
  * Developer Advocacy
    * Upcoming friday next meetup
    * Jan-Gerke will demo how to use cypress
    * Last time Birk gave a demo of the app hub
      * Some external devs were really engaged (:thumbsup:)
    * Developer portal: Would be nice to add google analytics
      * Could use an alternative solution, e. g. the one the Android team uses
        * matomo.org
    * Some guides in the repo have been added
    * There are some volunteers on github that will help with the documentation
  * Client-side caching meeting
    * Outcome of the proposals:
      https://github.com/dhis2/notes/blob/master/minutes/2021/06/03-client-side-caching.md
    * Using react-query inside app-runtime
    * Next step: Expand on proof of concept
      * starting next week
    * Nice to have: Figure out possible interations between pwa caching and
      app-runtime caching
    * Ideally no breaking changes, will be released on alpha to be able to play
      around with it
  * PR Previews
    * New workflows available, can be [installed with
      `d2-style`](https://dhis2.slack.com/archives/C0BP0RABF/p1622810229070700) 
    * To do: updating the default CORS whitelist in databases and environments.
    * Example workflow:
      https://github.com/dhis2/workflows/blob/master/ci/dhis2-preview-pr.yml
    * One caveat: Only a labeled event will trigger the deploy. And that means
      that if you pushed new changes after you have deployed a preview you need
      to remove the label and then add the label back to trigger the event
      again.
  * Visual regression
    * Debora, Ismay & Medi are working on solutions
  * CI/CD
    * Updates regarding app versions, see above
    * Workflow updates improve performance on CI
  * i18n
    * Working grouped should at how transifex works
      * Talk to Phil to get connected with the translators and get an
        introduction how they work with transifex
  * Browserlist
    * Nothing happened there
