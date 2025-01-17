---
title: Dark Mode
---

<head>
  <title>Dark Mode to Change Color Schemes and CSS Properties</title>
  <meta
    name="description"
    content="Developers are adding dark mode CSS on native applications to support their user preferences. Read to learn more about dark color schemes for Ionic apps."
  />
</head>

Ionic makes it easy to change the themes of your app, including supporting dark color schemes. Dark mode is a display setting that changes all of an app's views to a dark theme. It has system-wide support on iOS and Android, making it highly desirable for developers to add to their apps.

## Using Media Queries

The modern way to enable dark mode is by using the [CSS media query for the user's preferred color scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme). This media query will hook into the system setting of the user's device and apply the theme if dark mode is enabled. Ionic Framework starters use this method to include the dark theme.

```css
@media (prefers-color-scheme: dark) {
  :root {
    /* Dark mode variables go here */
  }
}
```

The `prefers-color-scheme` media query is supported by [all modern browsers](https://caniuse.com/#feat=prefers-color-scheme). Users will not be able to benefit from having the dark theme applied using this media query in certain browsers, however, the dark theme can still be applied by using a [CSS class fallback](#css-class-fallback) if support for older browsers is needed.

## CSS Class Fallback

As a fallback method for devices that don't support the media query, the dark mode can be applied by styling a CSS selector and applying the class to the document body.

```css
@media (prefers-color-scheme: dark) {
  :root {
    /* Dark mode variables go here */
  }
}

/* Fallback for older browsers or manual mode */
body.dark {
  /* Dark mode variables go here */
}
```

With the variables targeting the `body.dark` selector, all that is needed now is to add the class to the `<body>` in the app. This can be done in a variety of ways depending on the framework your app is built with.

Notice that the variables should be in both places in this example. We can [use JavaScript](#combining-with-javascript) in order to avoid setting the variables in two places.

## Combining with JavaScript

In order to keep the CSS variables written once and avoid having to update them in multiple places, the `dark` class can be added when the value of the `prefers-color-scheme` media query is `dark`. Here's what the CSS would look like:

```css
body.dark {
  /* Dark mode variables go here */
}
```

Notice that the variables above are only in the `body.dark` selector now, and the `prefers-color-scheme` media query has been removed.

### Automatically Enable Dark Mode

The `dark` class can be added to the `<body>` by checking if the document matches the media query using [matchMedia()](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia). This will allow dark mode to still work based on the user's preference.

:::note
The demo below prioritizes the site's theme over the system settings. If your system settings are set to something other than the site's theme when the demo loads, it will match the site's theme. Try changing the system preferences on your device between light & dark mode to see it change.
:::

:::info
Not sure how to change the system settings? Here's [how to enable dark mode on Windows 11](https://support.microsoft.com/en-us/windows/change-colors-in-windows-d26ef4d6-819a-581c-1581-493cfcc005fe) and [how to enable it on a Mac](https://support.apple.com/en-us/HT208976).
:::

import AutomaticDarkMode from '@site/static/usage/v7/theming/automatic-dark-mode/index.md';

<AutomaticDarkMode />

### Manually Toggle Dark Mode

In addition to adding the `dark` class to the `<body>` when the media query changes, the class can be added by the app, such as when a user changes a toggle, to switch between the light and dark themes:

import ManualDarkMode from '@site/static/usage/v7/theming/manual-dark-mode/index.md';

<ManualDarkMode />

## Adjusting System UI Components

When developing a dark theme, you may notice that certain system UI components are not adjusting to dark mode properly. To fix this you will need to specify the `color-scheme`. See the <a href="https://caniuse.com/#feat=mdn-html_elements_meta_name_color-scheme" target="_blank">browser compatibility for color-scheme</a> for details on cross browser support.

While you may be mainly using Ionic components instead of only native components, `color-scheme` can also affect aspects of your application such as the scrollbar. In order to use `color-scheme` you will need to add the following HTML to the `head` of your application:

```html
<meta name="color-scheme" content="light dark" />
```

This allows the page to indicate which color scheme it is comfortable being rendered with. Alternatively, you can add the following CSS to do this on a per-element basis:

```css
color-scheme: light dark;
```

| Default scrollbar                                                        | Scrollbar with `color-scheme`                                        |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| ![Application without color-scheme](/img/theming/color-scheme-light.png) | ![Application with color-scheme](/img/theming/color-scheme-dark.png) |

For more information regarding `color-scheme` please see https://web.dev/color-scheme/.

:::note
`color-scheme` does not apply to the keyboard. For details on how dark mode works with the keyboard, see [Keyboard Documentation](../developing/keyboard.md#dark-mode).
:::

:::note
For developers looking to customize the theme color under the status bar in Safari on iOS 15 or the toolbar in Safari on macOS, see [`theme-color` Meta](./advanced.md#theme-color-meta).
:::

## Ionic Dark Theme

Ionic has a recommended theme for variables to use in order to get a dark mode based on the device running the app. It can be broken down into the following parts:

1. Changing the default [Ionic colors](colors.md) for all [modes](platform-styles.md#ionic-modes) to complement the dark background in the `body.dark` selector.
2. Setting variables for the dark theme on `ios` devices.
3. Setting variables for the dark theme on `md` devices.

The following code can be copied and pasted into an app's global CSS file to get Ionic's dark theme. We are [using the CSS media query](#using-media-queries) to enable dark mode. If older browser support is required, use the method described in the [combining with JavaScript](#combining-with-javascript) section.

:::info
For more information on the variables that are being changed, including other variables that can be added to further customize, see [Themes](themes.md).
:::

```css
@media (prefers-color-scheme: dark) {
  /*
   * Dark Colors
   * -------------------------------------------
   */

  body {
    --ion-color-primary: #428cff;
    --ion-color-primary-rgb: 66, 140, 255;
    --ion-color-primary-contrast: #ffffff;
    --ion-color-primary-contrast-rgb: 255, 255, 255;
    --ion-color-primary-shade: #3a7be0;
    --ion-color-primary-tint: #5598ff;

    --ion-color-secondary: #50c8ff;
    --ion-color-secondary-rgb: 80, 200, 255;
    --ion-color-secondary-contrast: #ffffff;
    --ion-color-secondary-contrast-rgb: 255, 255, 255;
    --ion-color-secondary-shade: #46b0e0;
    --ion-color-secondary-tint: #62ceff;

    --ion-color-tertiary: #6a64ff;
    --ion-color-tertiary-rgb: 106, 100, 255;
    --ion-color-tertiary-contrast: #ffffff;
    --ion-color-tertiary-contrast-rgb: 255, 255, 255;
    --ion-color-tertiary-shade: #5d58e0;
    --ion-color-tertiary-tint: #7974ff;

    --ion-color-success: #2fdf75;
    --ion-color-success-rgb: 47, 223, 117;
    --ion-color-success-contrast: #000000;
    --ion-color-success-contrast-rgb: 0, 0, 0;
    --ion-color-success-shade: #29c467;
    --ion-color-success-tint: #44e283;

    --ion-color-warning: #ffd534;
    --ion-color-warning-rgb: 255, 213, 52;
    --ion-color-warning-contrast: #000000;
    --ion-color-warning-contrast-rgb: 0, 0, 0;
    --ion-color-warning-shade: #e0bb2e;
    --ion-color-warning-tint: #ffd948;

    --ion-color-danger: #ff4961;
    --ion-color-danger-rgb: 255, 73, 97;
    --ion-color-danger-contrast: #ffffff;
    --ion-color-danger-contrast-rgb: 255, 255, 255;
    --ion-color-danger-shade: #e04055;
    --ion-color-danger-tint: #ff5b71;

    --ion-color-dark: #f4f5f8;
    --ion-color-dark-rgb: 244, 245, 248;
    --ion-color-dark-contrast: #000000;
    --ion-color-dark-contrast-rgb: 0, 0, 0;
    --ion-color-dark-shade: #d7d8da;
    --ion-color-dark-tint: #f5f6f9;

    --ion-color-medium: #989aa2;
    --ion-color-medium-rgb: 152, 154, 162;
    --ion-color-medium-contrast: #000000;
    --ion-color-medium-contrast-rgb: 0, 0, 0;
    --ion-color-medium-shade: #86888f;
    --ion-color-medium-tint: #a2a4ab;

    --ion-color-light: #222428;
    --ion-color-light-rgb: 34, 36, 40;
    --ion-color-light-contrast: #ffffff;
    --ion-color-light-contrast-rgb: 255, 255, 255;
    --ion-color-light-shade: #1e2023;
    --ion-color-light-tint: #383a3e;
  }

  /*
   * iOS Dark Theme
   * -------------------------------------------
   */

  .ios body {
    --ion-background-color: #000000;
    --ion-background-color-rgb: 0, 0, 0;

    --ion-text-color: #ffffff;
    --ion-text-color-rgb: 255, 255, 255;

    --ion-color-step-50: #0d0d0d;
    --ion-color-step-100: #1a1a1a;
    --ion-color-step-150: #262626;
    --ion-color-step-200: #333333;
    --ion-color-step-250: #404040;
    --ion-color-step-300: #4d4d4d;
    --ion-color-step-350: #595959;
    --ion-color-step-400: #666666;
    --ion-color-step-450: #737373;
    --ion-color-step-500: #808080;
    --ion-color-step-550: #8c8c8c;
    --ion-color-step-600: #999999;
    --ion-color-step-650: #a6a6a6;
    --ion-color-step-700: #b3b3b3;
    --ion-color-step-750: #bfbfbf;
    --ion-color-step-800: #cccccc;
    --ion-color-step-850: #d9d9d9;
    --ion-color-step-900: #e6e6e6;
    --ion-color-step-950: #f2f2f2;

    --ion-item-background: #000000;

    --ion-card-background: #1c1c1d;
  }

  .ios ion-modal {
    --ion-background-color: var(--ion-color-step-100);
    --ion-toolbar-background: var(--ion-color-step-150);
    --ion-toolbar-border-color: var(--ion-color-step-250);
  }

  /*
   * Material Design Dark Theme
   * -------------------------------------------
   */

  .md body {
    --ion-background-color: #121212;
    --ion-background-color-rgb: 18, 18, 18;

    --ion-text-color: #ffffff;
    --ion-text-color-rgb: 255, 255, 255;

    --ion-border-color: #222222;

    --ion-color-step-50: #1e1e1e;
    --ion-color-step-100: #2a2a2a;
    --ion-color-step-150: #363636;
    --ion-color-step-200: #414141;
    --ion-color-step-250: #4d4d4d;
    --ion-color-step-300: #595959;
    --ion-color-step-350: #656565;
    --ion-color-step-400: #717171;
    --ion-color-step-450: #7d7d7d;
    --ion-color-step-500: #898989;
    --ion-color-step-550: #949494;
    --ion-color-step-600: #a0a0a0;
    --ion-color-step-650: #acacac;
    --ion-color-step-700: #b8b8b8;
    --ion-color-step-750: #c4c4c4;
    --ion-color-step-800: #d0d0d0;
    --ion-color-step-850: #dbdbdb;
    --ion-color-step-900: #e7e7e7;
    --ion-color-step-950: #f3f3f3;

    --ion-item-background: #1e1e1e;

    --ion-toolbar-background: #1f1f1f;

    --ion-tab-bar-background: #1f1f1f;

    --ion-card-background: #1e1e1e;
  }
}
```
