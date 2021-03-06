# React CSS Theming (with JS objects)

This tiny 500byte (not gzipped) component allows JS theme objects to be passed into your component where they're converted into CSS Variables for internal use.

<h2>Demo</h2>

https://codesandbox.io/s/react-js2css-theme-demo-s6xlx

<h2>Why?</h2>

- Switching CSS Variables for themes is unpleasant for users of your component, JS objects are easier to deal with.

- CSS Variable changes are much faster than React re-renders via Context which is what CSS-in-JS solutions do.

- If you care about performance and bundle size and want to avoid CSS-in-JS solutions altogether you can still provide a nice JS theme object interface to your users.

## Install

```
yarn add react-js2css-theme
```

<h2>Usage</h2>

```js
const yourTheme = {
  background: 'black',
  textColor: 'white',
  fontFamily: '"Roboto", sans-serif',
  fontWeight: 500,
  button: {
    padding: '10px',
  },
};
```

<h3>As a component</h3>

```js
import JSToCSSTheme from 'react-js2css-theme';

<JSToCSSTheme namespace="xx" theme={yourTheme}>
  <YourComponent />
</JSToCSSTheme>;
```

<h3>As a hook</h3>

You may not wish to create an extra wrapping element, in this case you can use the hook:

```js
import { useJsToCss } from 'react-js2css-theme';

function YourComponent() {
  const themeStyle = useJsToCss('xx', yourTheme);

  return (
    <div>
      <style>{themeStyle}</style>
      {/* ... your component JSX */}
    </div>
  );
}
```

Your component can now make use of the following CSS Variables:

```css
:root {
  --xx-background: black;
  --xx-textColor: white;
  --xx-fontFamily: 'Roboto', sans-serif;
  --xx-fontWeight: 500;
  --xx-buttonPadding: 10px;
}
```

Now try changing the theme object and watch your component's theme change :)

<h2>Requirements</h2>

- All browsers except IE
