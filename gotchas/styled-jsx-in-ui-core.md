# Usage of styled-jsx in our ui-core library

With styled-jsx, for our components in ui-core:

- We try to target the element (e.g. https://github.com/dhis2/ui-core/blob/master/src/Button/styles.js#L6)
- Sometimes we cannot do that, e.g. if we have nested div elements, then we use cx('root', className) and add the .root to the outermost div
- We accept that styles may bleed into our components if the consumer is using global styles (https://github.com/dhis2/ui-core#how-to-avoid-a-global-style-rule-from-affecting-a-ui-core-component)
- We guarantee that our components will never bleed out styles to other components
- We use the className prop to allow overrides from a consumer, and we attach the className prop to the outermost element of our component
