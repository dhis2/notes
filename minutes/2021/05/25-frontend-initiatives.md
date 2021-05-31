# Frontend Initiatives Meeting

**When**: May 25, 2021 15:00 CET
**Who**: Austin, Birk, Debora, Edoardo, Hendrik, Ismay, Jan O, Jan-Gerke, Jennifer, Joakim, Kai, Martin, Medi, Simona, Viktor

## Agenda

- General updates

  - GitHub changed the Personal Access Token formats so they need to be regenerated in the new format. If there are any problems related to dhis2-bot not having access, let us know.
  - Recommend backing off the amount of open PRs Dependabot maintains in one update cycle. They are using a lot of resources right now when they rebase and all workflows run again.
  - We are looking at visual regression testing solutions for e.g. UI. If anyone has practical experience with e.g. Percy, Chromatic, or others, let us know and we'd love to pick your brain a bit !
  - DataTable PR status
  - Browserlist support needs to be defined.
  - Rolling meeting notes for UI meetings?
- Working group updates
  - PWA
  - Client-side caching
  - Cypress
  - PR deploy previews
  - CI/CD
  - Developer outreach
- Others?


## Notes

- PATs
  - If you see anything failing, let Viktor know
- Dependabot
  - Changed from 10 to 5 daily PRs to improve throughput of dependabot PRs
  - Currently ~160 open dependabot PRs across all repos, need to have a strategy to keep under control
  - If you run into challenges, bring them up so we can adjust the throttling
- Visual regression testing tools
  - Anyone have experience with ~~Checkly~~, Percy, Chromatic?  Reach out!
  - Ismay has some experience with both
  - **Task: ** up a working group to take holistic view of decision
    - @Ismay (lead)
    - @Medi
    - @Debora
- DataTable PRs
  - ~ next week - Blocked by UI restructure decision
  - **Task:** set meeting to go over PR
    - Scheduled for tomorrow at 14-15h
-  Browserlist Config
  - Opera Mini features aren't being polyfilled?
  - Should we remove it?
  - **Task:** create a working group to re-evaluate browserlist with 
    - Split out into shareable config package (see Data)
    - Consider shareable config for other tools (babel, rollup, browserslist, jest, eslint, prettier, etc.)
    - @Austin (lead)
    - @Ismay
    - @Viktor
- **Task:** move to Rolling Notes (Viktor, Austin)
  - Consider how this interfaces with version control (if at all)

### Working Group Updates

- PWA
  - (@Kai) created a proof of concept in app-platform [branch](https://github.com/dhis2/app-platform/tree/feat-add-service-worker) connecting React API with service worker
  - Kai gave an awesome demo!!
  - Next step: some design decisions on shell/runtime split and alerts for online/offline
- Client-side caching
  - Nothing really new to report
  - Meeting next week
  - Decide on an approach to take (useSWR, react-query)
  - Keep PWA normalization in mind as we build client-side caching (and vice-versa)
- Cypress
  - Upgraded cypress version
  - Some issues remain with intercept conflicts between cucumber and vanilla cypress
  - Working on it...
  - What is our long-term vision on Cucumber
  - **Task:** time for a follow-up meeting on Cucumber/Cypress [issue #136](https://github.com/dhis2/notes/issues/136)
    - Have two proposals ready?
    - @Viktor to organize
- PR Previews
  - Merged into Capture App
  - Whitelisting not yet in place 
  - **Task:** follow-up with Phil to script adding netlify URLs to whitelist
    - @Austin
- AppHub, CI/CD
  - Good to go with the redesign
  - Merged to staging, should merge to master soon
  - Birk gave an awesome demo!
  - App Platform publish PR - should merge soon!
- Developer Outreach
  - Meetup scheduled for Friday, need to select a topic
    - Security & Performance
    - Cypress
    - Android
  - Updating developer portal
    - More guides coming
    - Masters students MIA?
    - Contributing guide coming soon
- i18n
  - Set up interviews / focus groups with translators?
  - **Task: ** working group start with meeting with Phil
    - @Viktor (lead)
    - @Martin

