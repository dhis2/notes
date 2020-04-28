Date: 2020-04-28\
Attendees: Ismay, Jan-Gerke, Viktor

# Agenda

Simplification and consistency of the form controls, e.g. Radio, Checkbox, Switch, Field, *Field-components.

Touched on future changes we want to explore for ui@6 as well.

# @dhis2/ui-core

-   Drop the Field component

-   Re-implement as a [generic form
    field](https://github.com/dhis2/ui/pull/46/files#diff-0556b6ad0bddb321a9ddd41f13279cb6R31-R48)
    that adds the status, help, validation texts in a consistent way.

-   Refactor all *Field components to use re-implemented Field

-   Move as *Field components to widgets

# @dhis2/ui-widgets

- Provide default translations and strings

# @dhis2/ui-forms

-   Use more explicit style for controls instead of e.g. `options`.
    Instead of using e.g. `RadioGroupControl` and provide an array of
    plain JavaScript options: `[ { value, label }, ... ]` and handle the
    [checked state
    internally](https://github.com/dhis2/ui/blob/alpha/packages/core/src/ToggleGroup/ToggleGroup.js#L37-L39)
    we leverage the functionality that FinalForm provides by using the
    format:

    ```js
    <Field
        type="radio"
        component={RadioControl}
        name="choice"
        label="One"
        value="one"
    />
    <Field
        type="radio"
        component={RadioControl}
        name="choice"
        label="Two"
        value="two"
    />
    ```

-   Require consumers to specify type="radio" or "checkbox".
    This allows us to mix components within the same group:

    ```js
    <Field type="checkbox" component={CheckboxControl} name="group-one" label="cat" />
    <Field type="checkbox" component={CustomCheckboxControl} name="group-one" label="dog" />
    ```

    And, it allows us to use the same style of event handlers, and can
    leverage built-in functionality in FinalForm to provide e.g. boolean
    vs. string values.

-   Component that can show error messages for a group.

-   Propose to rename the forms components to have e.g. FF as a suffix: `InputFieldFF`, `TextAreaFieldFF`, etc.

# Future

- Propose to drop all external margins from our components.
- Propose to move back to string based props for status and variants: `status="error"` and `variant="primary"`.
- React-like vs. HTML-like API: https://github.com/dhis2/ui/issues/29
