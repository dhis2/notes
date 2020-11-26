**Date**: 2020-11-25

**Attending**: Viktor, Austin, Jan-Gerke, Ismay

## Notes

Meeting about this PR https://github.com/dhis2/usage-analytics-app/pull/388 and the things that came up during the review. This report is just so that everyone can reviews the notes, after that we can move the remaining topics to Jira issues if we all agree. That way we can delay the non-critical work, so that we don’t have to deal with it all in a single PR.

### Address later

- Use only named exports vs use both default and named exports. We don’t yet have a convention on this, might be good to see if we want to recommend one or the other.
- Instead of the components, selectors and constants folders, move it all into the components folder (and maybe move that folder as well). So that we have a consistent organisation of files.
- Abstract the data fetching logic in the Query components into separate hooks.
- Do the checks for the stale data when the interval changes in the fetching hooks, instead of in other areas of the app.
- Use `__test__` folders instead of co locating tests with the tested files.
- Update all dependencies (which would also address the cli style import sorting).
- See if the state variables in the App.js component could be simplified a bit. There are quite a lot of them currently.
- Parameter destructuring, should we destructure so it’s explicit, or pass params without destructuring for brevity (no conclusion yet)?
- Some idiosyncracies that ended up in the refactor could probably have been avoided if multiple people had been involved from the start, like with the sms app refactor. Not much we can do about that now, but good to keep in mind for the future.

### Address in the PR

- Rename interval and setInterval (so we don’t shadow the global setInterval).
- Use css variables for the colors.
- Remove css reset and body styles.
