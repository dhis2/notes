Date: 2021-03-02

Attending: Austin, Birk, Christos, Hendrik, Ismay, Jennifer, Martin,
Médi-Rémi, Debora, Kai, Edoardo, Viktor

## Notes

### Large push to App Platform last week

### Working groups

#### PWA & Data Caching - call for task force members

-   Updates to header bar
-   PWA in the shell
-   Data caching with service worker
-   Changes to the UI in the dashboard
    Sync status, online/offline

**Task Force**: Jennifer, Médi-Rémi, Austin, (Jan Henrik), Kai

#### App Runtime - field & paging warnings

Last week we merged a change to App Runtime and is available through the
App Platform that console logs a warning on development runtime when
fields and/or paging is misused by e.g. specifying paging=false, and/or
fields not being specific enough.

**Don't ignore warnings** -- this will break in the future. Report them
in JIRA or fix them.

Please report false positives so we can fix them in the app-runtime.

#### App Hub Updates

Quick demo. Released from next to master on Friday.

-   Implemented paging.
-   New auth flow.
-   Developer API key generation.

#### Quick demo of publish command

-   New publish command that publishes an app to the platform.
-   The app needs to exist on App Hub, so needs to be manually created
    first.
-   The `id` needs to be in the `d2.config.js`
-   `app-scripts publish --api-key KEY`
-   Will be integrated in the semantic-release (`d2-utils release`)

### Topics

#### PR Previews @paschalidi

Update with our options: https://github.com/dhis2/notes/discussions/183#discussioncomment-469400

Push to get Netlify running.

If we cannot get funding for Netlify move on Surge.

Viktor follows up.

#### Web Development Academy

-   (add links to join)
