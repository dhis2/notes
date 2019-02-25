# `dhis2/ui` feedback meeting

## Attending

- austin
- hendrik
- jennifer
- viktor

## Re-export files

- Webpack 4 implements strict es modules for mjs files
- Unclear if that's an actual specification

**Investigation results**: 

The eco-system surrounding JavaScript modules is split but there is work
to bring the two biggest ones: ECMAScript modules and CommonJS, closer
together[1].

Webpack 4 has implemented something called strict-ESM, which basically
enforces[2]:

>Dynamic modules (non-esm, i. e. CommonJs) can only imported via default
>import, everything else (including namespace import) emit errors

There is additional information straight from the webpack team in [3] as
well: 

>webpack supports the `__esModule` flag, with upgrades a CJS module to a ESM.

It does not upgrade a `__esModule` module to a strict-ESM module
however:

>In strict-ESM we don’t allow picking properties via `import` and only
>allow the default export for non-ESM.

This breaks in UI.

- [1] https://github.com/nodejs/modules
- [2] https://medium.com/@zwegrzyniak/webpack-4-1-and-es-modules-esm-dd0bd7dca4da
- [3] https://medium.com/webpack/webpack-4-import-and-commonjs-d619d626b655

**Conclusion**: Now that the cause is clear, we need to decide on what
direction to take with the UI-library. All the approaches have drawbacks.
One thing is clear, if we are going to use ESM compiled to CJS as it
stands today, we do not use `.mjs` as the file extension.

- _Action_: Merge PR: https://github.com/dhis2/ui/pull/140

## Fonts

- The application font will be used by the application as well as the
  components
- We don't want to run the risk of bundling it twice or defining it
  twice

**Conclusion**:

- Use MDIDX for icons for v1.0
- As an optimization step we should switch to SVGs, this triggers
  changes in the `Icon` component, but it should be a non-breaking
  change.
- The host application will pull in application level fonts (e.g.
  Roboto), but would be nice to throw some sort of error if it doesn't.
- The UI components expect that the font is loaded by that application
  and just defines the `font-family` it needs

## Feedback

Input from the field.

### Down-side of isolated styles

- Difficult to re-use primitives of styles

**Note**:

- Some of the primitives, for example the colors, are exposed from the
  UI library as CSS, which can be imported and re-used.

**Conclusion**: This is something to watch out for. If this setup adds
duplication of colors and standard styles throughout all applications we
need to change it in `dhis2/ui`.

### Down-side of locked down apis

- No paddings/margins atm, so everything has been wrapped in another
  components to allow for whitespace.

**Conclusion**:

- There is a design for a grid system which allows a whitelisted set of
  values for e.g. padding/margins which we need to document and
  implement.

- _Action_: Viktor to follow up with Joe and implement the required props.

### Experience with implementing headerbar

- The UI component broke stuff, then it broke again when it was removed.

- Translations not included with the headerbar

- The headerbar currently causes everything in UI to be bundled.

**Conclusion**:

- The translations for the headerbar should absolutely be included with
  the headerbar component

- Migrate the header-bar to d2-ui-header-bar

- Make sure the headerbar is tree-shakeable, currently it does named
  imports from core which is not tree-shakeable as we use ESM->CJS
  modules.

- For apps which have implemented the new headerbar, an upgrade to the
  beta version on NPM is preferable.

- Make the app search keyboard friendly, so it's possible to tab between
  the apps in the list.

- _Action_: Viktor to clean up headerbar (tree-shakability) and migrate it
  to d2-ui.

## Testability for browser tests:

- E2E-tests requires a stable way to target the DOM
- UI components could have a test-id

**Conclusion**:

- Not a good idea to hard code a test-id on the components, as e.g. a
  form might have multiple buttons and if they have the same id it is
  impossible to determine e.g. which of the buttons submit the form and
  which cancels it.

- `data-test-id` on component, pass through the property to the
  component itself.

- _Action_: Viktor to add the prop.

## Standard API

The API should be consistent between components so there is a transfer
of knowledge. E.g. once you learn the API for one component some of that
knowledge should be applicable to other components as well.

**Conclusion**:

- We want a standard set of properties for all components

- Not duplicate all the props on each component

- Use a composable structure

- Locked down API to start, open up when there's a real need

## Future ideas

- UI components could delegate the processing the requests to the
  application

  - simple: pass in pre-configured callbacks to the components for the
    data

  - sophisticated: design a system which would allow the components to
    define what data they need (ref. apollo client, graphql, etc.):

    ```
    <Query query="{ user { name } }"> ({ loading, error, data }) => { if (error) return error; if (loading) return '...'; return <span>{data}</span> } </Query>
    ..
    <Query resource="analytics/event" filter="xxx">
    ```

- UI components could be configured to know where they get external data
  from

- Complex components could provide reducers/actions for the apps to hook
  into the state of the component

- ui: not coupled to dhis2

- d2-ui: coupled with dhis2

## Next steps

- Start to investigate if dashboards can use some components

- React v17 will drop the legacy context api completely, but quite a few
  d2-ui components rely on this. We need a strategy for dealing with
  that scenario.

## Side discussions

Important for all apps, and should be addressed in a another meeting as
they are out of scope for the `dhis2/ui` discussion.

### Accessibility

- make sure tabs works
- aria labels
- etc.

### Translations

- how would a user contribute with translations for his language?
