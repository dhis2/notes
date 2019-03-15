# Redux conventions

Based on the discussion about [prefixing action
types](https://github.com/dhis2/notes/issues/18) some conventions can be
extracted for how to use Redux.

Austin mentioned an article about [Redux best
practices](https://medium.com/@kylpo/redux-best-practices-eef55a20cc72)
which we can use as inspiration.

## Utilities

- Use [redux-actions](https://github.com/redux-utilities/redux-actions)
  to create and handle actions.

- Use [redux-thunk](https://github.com/reduxjs/redux-thunk) to deal with
  logic that has side-effects (e.g. async code, api requests).

- Use [reselect](https://github.com/reduxjs/reselect) for memoized
  selectors.

## Principles

- **Reducers**: are
  [deterministic](https://github.com/reduxjs/redux/issues/1171#issuecomment-205888533)
  and pure.

- Use **Selectors** to compute derived data.

- **Compose reducers**:
  > Think of Redux as a tree of your reducers (like react’s render tree
  > of components). Both are just compositions of functions.

- Normalize API responses to create domain specific reducers with e.g.
  [normalizr](https://github.com/paularmstrong/normalizr).

## Naming

- Action name: `<NOUN>_<VERB>`
  e.g. `REPORT_COLLABORATOR_PERMISSIONS_ADD`, `REPORT_DATA_FETCH`

- Action creator name: `<verb><Noun>`
  e.g. `activateFilter`, `fetchReportData`

- Selector name: `get<Noun>`
  e.g. `getReportData()`, `getActiveFilter()`

> **Note:** Use the **imperative** form of the verb in your actions so
> each action reads like a command.
>
> e.g. `ADD` not `ADDED`, `FETCH` not `FETCHED`.

## State

Think about what state to put in the Redux store. There are no hard and fast
rules for this.

Read [Redux FAQ about organizing
state](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-react-s-setstate)
for some pointers on how to think about state management.

> Using local component state is fine. As a developer, it is your job to
determine what kinds of state make up your application, and where each piece of
state should live. Find a balance that works for you, and go with it.
>
> Some common rules of thumb for determining what kind of data should be put
into Redux:
> 
> - Do other parts of the application care about this data?
> - Do you need to be able to create further derived data based on this
original data?
> - Is the same data being used to drive multiple components?
> - Is there value to you in being able to restore this state to a given point
in time (ie, time travel debugging)?
> - Do you want to cache the data (ie, use what's in state if it's already
there instead of re-requesting it)?
> - Do you want to keep this data consistent while hot-reloading UI components
(which may lose their internal state when swapped)?

There are [performance implications of how you organize your
store](https://redux.js.org/faq/organizing-state#should-i-put-form-state-or-other-ui-state-in-my-store),
so think about those use-cases as well:

> If you are keeping form state in Redux, you should take some time to
> consider performance characteristics. Dispatching an action on every
> keystroke of a text input probably isn't worthwhile, and you may want
> to look into ways to buffer keystrokes to keep changes local before
> dispatching. As always, take some time to analyze the overall
> performance needs of your own application.


## Future

- [Dynamic action
  naming](https://github.com/dhis2/notes/issues/18#issuecomment-466974138)
  could be useful to enable functionally isolated components to hook
  into the application Redux store, which would allow for these
  components to interact without knowing about each other beforehand.
  This could allow us to compose entire applications based on these
  components.
