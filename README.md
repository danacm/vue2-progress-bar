# vue2-progress-bar [![npm package](https://img.shields.io/npm/v/vue2-progress-bar.svg)](https://www.npmjs.com/package/vue2-progress-bar)

> A linear progress bar component for Vue.js. Uses SVG and javascript to animate a radial progress bar with a gradient.

[Live Demo](https://danacm.github.io/vue2-progress-bar)

# Requirements

- [Vue.js](https://github.com/vuejs/vue) `^2.0.0` (Compatible with Vue 1.0 or 2.0)
- A module bundler such as [webpack](https://github.com/webpack/webpack) or use the minified version on its own.

# Installation

```bash
$ npm install --save vue2-progress-bar
```

# Usage

```html
<template>
  <progress-bar
    :diameter="200"
    :completed-steps="completedSteps"
    :total-steps="totalSteps"
  >
    <template v-slot:header>this is header slot </template>
    <template v-slot:footer> this is footer slot</template>
    <template v-slot:tip> {{(completedSteps/totalSteps)*100}}%</template>
  </progress-bar>
</template>

<script>
  import ProgressBar from "vue2-progress-bar";

  export default {
    data() {
      return {
        completedSteps: 0,
        totalSteps: 10
      };
    },
    components: {
      ProgressBar
    }
  };
</script>
```

# Props

| Name               | Default value | Description                                                                                                                                                                  |
| ------------------ | :-----------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `height`           |     `10`      | Height of the progress bar in pixels.                                                                                                                                        |
| `width`            |     `10`      | Width of the progress bar in pixels.                                                                                                                                         |
| `totalSteps`       |     `10`      | Total number of steps to complete progress bar.                                                                                                                              |
| `completedSteps`   |      `0`      | Number of completed steps in the progress bar.                                                                                                                               |
| `startColor`       |   `#73cbfe`   | The color of the leading edge of the progress bar gradient.                                                                                                                  |
| `stopColor`        |   `#458efd`   | The secondary color of the progress bar gradient.                                                                                                                            |
| `innerStrokeColor` |   `#d6efff`   | Background color of the progress bar.                                                                                                                                        |
| `strokeLinecap`    |    `round`    | The type of stroke linecap for circle.                                                                                                                                       |
| `animateSpeed`     |    `1000`     | The amount of time in milliseconds to animate one step.                                                                                                                      |
| `timingFunc`       |   `linear`    | The transition timing function to use for the CSS transition. See [transition-timing-function](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function). |
| `showTip`          |    `true`     | Show tip text after the progress bar.                                                                                                                                        |

# Slot

| Name     |        Default value        | Description                              |
| -------- | :-------------------------: | ---------------------------------------- |
| `header` |           `null`            | header slot of the progress bar .        |
| `footer` |           `null`            | footer slot of the progress bar.         |
| `tip`    | `completedSteps/totalSteps` | tip content slot after the progress bar. |

# Dev

> npm run dev

## 📒 ChangeLog

[ChangeLog](./CHANGELOG.md)

# License

[The MIT License](LICENSE)
