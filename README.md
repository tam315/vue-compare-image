# Vue Compare Image

Simple Vue component to compare two images using slider.

![img](https://react-compare-image.yuuniworks.com/anime.gif)

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

```cmd
yarn add vue-compare-image

// or

npm install --save vue-compare-image
```

```js
import VueCompareImage from 'vue-compare-image';

<VueCompareImage leftImage="image1.jpg" rightImage="image2.jpg" />;
```

## Props

| Prop (\* required)       | type           | default | description                          |
| ------------------------ | -------------- | :-----: | ------------------------------------ |
| leftImage \*             | string         |  null   | left image's url                     |
| rightImage \*            | string         |  null   | right image's url                    |
| sliderLineWidth          | number (px)    |    2    | line width of slider (by pixel)      |
| handleSize               | number (px)    |   40    | diameter of slider handle (by pixel) |
| hover                    | boolean        |  false  | Whether to slide at hover            |
| sliderPositionPercentage | number (float) |   0.5   | Starting line position (from 0 to 1) |

## Dependencies

- [css-element-queries](https://github.com/marcj/css-element-queries) to detect element resize event.
