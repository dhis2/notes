# TL;DR (recommended setup)

### Usage of `styled-jsx` `css` and `css.resolve` function

In your code-base, make sure to call the `resolve` function directly, like so:

```javascript
import { resolve } from 'styled-jsx/css';
const buttonStyle = resolve`button { color: green; }`;
```

and not as property of the `css` function, i.e. **do not** do this:

```javascript
import css from 'styled-jsx/css';
const buttonStyle = css.resolve`button { color: green; }`;
```

### Mocking the `css` and `css.resolve` function

Create a mock file in the project root, adjecent to the `node_modules` folder: `./__mocks__/styled-jsx/css.js`

```javascript
module.exports.__esModule = true;
module.exports.default = () => 'default';
module.exports.resolve = () => 'resolve';
module.exports.global = () => 'global';
```

### Babel config

For the test env, include the `styled-jsx/babel-test` plugin, and make sure to exclude the `styled-jsx/babel` plugin:

```json
{
    "presets": ["react-app"],
    "env": {
        "production": {
            "plugins": ["styled-jsx/babel"]
        },
        "development": {
            "plugins": ["styled-jsx/babel"]
        },
        "test": {
            "plugins": ["styled-jsx/babel-test"]
        }
    }
}
```

# Background

The above setup is required to prevent a problem that arises when using calls to `css.resolve` in your code-base and then trying to mock the `css` function. In its original implementation in `styled-jsx`, `css` is a function, and to this function a property is added, a bit like this:

```javascript
function css() {}
css.resolve = function() {};
module.exports = css;
```

Now, this is quite irregular, but perfectly valid JavaScript, so it would be very logical to think that the mocked version could follow the same pattern. **However**, `jest` doesn't seem to have support for these type of functions. We haven't been able to get to the bottom of it, but we do know that trying to mock the function as above will just lead to `Cannot read propert "resolve" of undefined` errors in the tests.

By always calling the `resolve` function directly, and mocking the `css` function as in the recommended setup section, the above problem is circumvented.
