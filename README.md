# Vue Compare Image

[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors)

Simple Vue.js component to compare two images using slider.

![img](https://user-images.githubusercontent.com/10986861/67158760-0f02a480-f377-11e9-9b83-75bc8005693a.gif)

NOTE: [React Version](https://github.com/junkboy0315/react-compare-image) is also available!

## Demo

[DEMO](https://vue-compare-image.yuuniworks.com/)

## Features

- Simple
- Responsive (fit to the parent width)
- Size difference between two images handled correctly. Element size determined by following two factors:
  - width of the parent
  - right image's aspect ratio

## How to use

In the shell:

```bash
yarn add vue-compare-image

// or

npm install --save vue-compare-image
```

In your component file:

```js
import VueCompareImage from 'vue-compare-image';

export default {
  name: 'app',
  components: { VueCompareImage },
};
```

```xml
<template>
  <VueCompareImage leftImage="image1.jpg" rightImage="image2.jpg" />;
</template>
```

## Props

| Prop (\* required)       | type           | default | description                          |
| ------------------------ | -------------- | :-----: | ------------------------------------ |
| handleSize               | number (px)    |   40    | diameter of slider handle (by pixel) |
| hover                    | boolean        |  false  | Whether to slide at hover            |
| leftImage \*             | string         |  null   | left image's url                     |
| leftImageAlt             | string         |  null   | left image's alt                     |
| leftLabel                | string         |  null   | Left image text label                |
| rightImage \*            | string         |  null   | right image's url                    |
| rightImageAlt            | string         |  null   | right image's alt                    |
| rightLabel               | string         |  null   | Right image text label               |
| sliderLineWidth          | number (px)    |    2    | line width of slider (by pixel)      |
| sliderPositionPercentage | number (float) |   0.5   | Starting line position (from 0 to 1) |

## Dependencies

- [css-element-queries](https://github.com/marcj/css-element-queries) to detect element resize event.

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>
  <tr>
    <td align="center"><a href="https://www.yuuniworks.com/"><img src="https://avatars0.githubusercontent.com/u/10986861?v=4" width="100px;" alt="Shota Tamura"/><br /><sub><b>Shota Tamura</b></sub></a><br /><a href="https://github.com/junkboy0315/vue-compare-image/commits?author=junkboy0315" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/lukasirsak"><img src="https://avatars2.githubusercontent.com/u/30669262?v=4" width="100px;" alt="Lukáš Irsák"/><br /><sub><b>Lukáš Irsák</b></sub></a><br /><a href="https://github.com/junkboy0315/vue-compare-image/commits?author=lukasirsak" title="Code">💻</a></td>
  </tr>
</table>

<!-- ALL-CONTRIBUTORS-LIST:END -->
