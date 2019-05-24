# Front-end Decision Board, 2019-05-23

## #28 How do we add cli-style to repos

Considerations:

- Think about if the app is suitable for feature toggling as we are
  using it in a couple of places and getting some experience with good
  results.

- Be clear about pushing back on "backport everything, all the time",
  especially as we move forward on continuous app deployments.

**Conclusion**: We accept the proposal outlined.

## #24 Use github's stale bot / autoresponder / etc.

**Conclusion**: OK to have these types of automations. Would be nice to
have issue templates to remind reporters about JIRA.

## #20 Move to a single d2-ui package

**Conclusion**: Move towards publishing @dhis2/d2-ui from a package with
a single entry-point so we can move to semantic releases for a better
workflow.

At the same time, let's clean up some deprecated components from d2-ui:

- `d2-ui-rich-text` can be moved to `ui-widgets`
- `d2-ui-tables` can be ported to `ui-core` and `ui-widgets` (depends on
  specs from Joe.
- `d2-ui-core` should be removed and components move to a MUI/ui-core
  hybrid until MUI can be refactored away.
- `d2-ui-header-bar` has been superseded by `ui-widgets`
- `d2-ui-forms` is planned to be replaced so remove it from `d2-ui`.
- `d2-ui-group-editor` only uses d2 for translations, should use
   `d2-i18n`.
- `d2-ui-icon-picker` only uses d2 for translations, should use
   `d2-i18n`.
- `d2-ui-legend` only uses d2 for translations and generateUid, needs
  refactor.
- `d2-ui-formula-editor` does not seem to be used, can be removed.
