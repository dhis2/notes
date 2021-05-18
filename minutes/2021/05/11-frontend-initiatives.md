# Frontend Initiatives Meeting

**When**: May 11, 2021 15:00 CET
**Who**: Austin, Birk, Bjørn, Debora, Edoardo, Hendrik, Ismay, Jan, Jan-Gerke, Jasmine, Jennifer, Joe, Kai, Martin, Médi, Simona, Viktor

## Agenda

https://github.com/dhis2/notes/discussions/283

- General
  - Plurals in i18n: [dhis2/app-platform#552](https://github.com/dhis2/app-platform/pull/552)
  - Workflow updates for forks/Dependabot: https://github.com/dhis2/workflows
  - cli-style version 8.x, beware of breaking changes: https://github.com/dhis2/cli-style/blob/master/CHANGELOG.md
  - Client-side caching approach discussion: [#282](https://github.com/dhis2/notes/discussions/282)
- Working groups
  - PWA
  - Cypress
  - CI/CD
- Other?

## Notes

* Plurals in i18n
  * Some languages have more than 2 plural forms
  * Solution: set defaultValue in `en.pot`
  * Released in next `@dhis2/app-platform`
  * Lots of cases where we're not doing plurals in DHIS2, we should be better
  * If you start using the new version and see any weirdness
  * Note: even if the singular case never appears, you need to include it
  * Note: don't concatenate strings, use interpolation instead!
  * TODO: add Context
  * TODO: confirm i18n RTL support
  * TODO: Create Transifex accounts for everyone
  * TODO: Coordinate with HISP groups 
* Dependabot workflow fix
  * New fix in `dhis2/workflows`
  * External PRs (including dependabot) cannot access secrets
  * For small Cypress test suites, could be run parallel (no API Key needed)
  * For forks there is an option to manually "trust" PRs ([GH blog](https://github.blog/2021-04-22-github-actions-update-helping-maintainers-combat-bad-actors/)) _but this doesn't grant access to secrets_
    * For context see [the github docs](https://docs.github.com/en/actions/managing-workflow-runs/approving-workflow-runs-from-public-forks)
    * Although workflows from forks do not have access to sensitive data such as secrets, they can be an annoyance for maintainers if they are modified for abusive purposes. To help prevent this, workflows on pull requests are not run automatically if they are received from first-time contributors, and must be approved first.

Basically GH blocks all workflows from running on PRs by first-time contributors. A manual approval button will be shown, which will allow the workflows to run (but still without secrets).
* New cli-style version
  * Run `d2-style check`, no need to run separately for `js` and `text` etc.
  * If there are any problems, open them in Jira CLI project / GH Notes Q&A / #d2 slack channel
  * See [CHANGELOG](https://github.com/dhis2/cli-style/blob/master/CHANGELOG.md) for more
* Client-side caching
  * Everyone should read up on [#282](https://github.com/dhis2/notes/discussions/282) and vote for their preferred solution
  * If you have questions or use-cases or additional suggestions, add them as new "solutions"
  * There is a meeting to discuss this Thursday next week (20/05 14:00) on frontend calendar, feel free to join!
* Updates - PWA
  * Service worker is working!
  * Will be adding documentation
  * Kai is working to confirm this
  * Next: how would this look with a dedicated service worker package
  * React API also in progress, will be working to integrate it with the service worker
* Network Shim
  * Upgraded to latest version of Cypress
  * Support "out-of-band" cy.intercept in node.js process
  * Ran into a bug in Cypress which was fixed
  * Found another bug in stub mode of Cypress, opened a PR 
  * Test suite almost complete (need to run in CI)
  * Next meeting: hopefully have a demo in SMS Config app
* CI / CD
  * Birk - App Hub, working on getting core apps up and running
  * Working on supporting "empty" apps (no version)
  * Working on validating uploaded app versions to ensure manifest data matches AppHub metadata
  * Redesign in testing, move to staging and then production soon
    * Have a proper workflow for organization invitations, can send emails from App Hub
  * Versioning of apps - proposal done, will be poste to Notes repo for feedback
  * App Management - blocked by upload of core apps to App Hub
    * Will be referring to core apps by ID, need to think about a better long-term strategy
* UI / DataTable
  * PR is basically ready, need to re-review with focus on API instead of on package structure
  * Long overdue, will try to get this in! (no date promised)
  * Maybe add `order:ASC` or something to the component API?
* PR previews
  * Approved and merged into Capture app
  * Need to update CORS whitelist in debug envs to support PR preview workflows
  * Two things needed to roll out to other applications (welcome to try this!)
    * Add NETLIFY_SITE_ID
    * Set up Workflow
    * Ping Viktor for help
  * Will try to script this to add to all app repos :muscle:
* GOTCHAS
  * Inconsistent handling of field names - short for GET, long for POST
    * i.e. [new DataValues API](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-236/data-validation.html#request-query-parameters)
    * To bring up 
* App Developer Academy
  * Completed last week, thanks to Debora, Kai, Médi, Jan-Gerke, and Hendrik!
  * Looking for ways to increase attendance and engagement 
