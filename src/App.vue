<template>
  <div class="demo-page">
    <h1>
      <a href="https://github.com/junkboy0315/vue-compare-image">Vue Compare Image</a>
    </h1>

    <pre class="code language-jsx">
      <code>
        {{ code1 }}
      </code>
    </pre>

    <div :style="{ maxWidth: '200px' }" class="container">
      <VueCompareImage leftImage="/cat1.jpg" rightImage="/cat2.jpg" rightImageAlt="alttttt" />
    </div>

    <pre class="code language-jsx">
      <code>
        {{ code2 }}
      </code>
    </pre>

    <div :style="{ maxWidth: '300px' }" class="container">
      <!-- eslint-disable-next-line -->
      <VueCompareImage
        leftImage="/forest1.jpg"
        rightImage="/forest2.jpg"
        :sliderPositionPercentage="0.2"
        leftLabel="Forest 1"
        rightLabel="Forest 2"
      />
    </div>

    <pre class="code language-jsx">
      <code>
        {{ code3 }}
      </code>
    </pre>

    <div :style="{ maxWidth: '500px' }" class="container">
      <VueCompareImage leftImage="/cat1.jpg" rightImage="/forest2.jpg" hover />
    </div>

    <pre class="code language-jsx">
      <code>
        {{ code4 }}
      </code>
    </pre>

    <div :style="{ maxWidth: '100%' }" class="container">
      <!-- eslint-disable-next-line -->
      <VueCompareImage
        leftImage="/forest1.jpg"
        rightImage="/cat2.jpg"
        :sliderLineWidth="5"
        :handleSize="80"
      />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import VueCompareImage from './VueCompareImage.vue';
import './assets/prism.css';
import './assets/prism';

const code1 = `
<div :style="{ maxWidth: '200px' }">
  <VueCompareImage
    leftImage="/cat1.jpg"
    rightImage="/cat2.jpg"
  />
</div>`;

const code2 = `
<div :style="{ maxWidth: '300px' }">
  <VueCompareImage
    leftImage="/cat1.jpg"
    rightImage="/cat2.jpg"
    :sliderPositionPercentage="0.2"
    leftLabel="Forest 1"
    rightLabel="Forest 2"
  />
</div>`;

const code3 = `
<div :style="{ maxWidth: '500px' }">
  <VueCompareImage
    leftImage="/cat1.jpg"
    rightImage="/cat2.jpg"
    hover
  />
</div>`;

const code4 = `
<div :style="{ maxWidth: '100%' }">
  <VueCompareImage
    leftImage="/cat1.jpg"
    rightImage="/cat2.jpg"
    :sliderLineWidth="5"
    :handleSize="80"
  />
</div>`;

export default Vue.extend({
  name: 'app',
  components: {
    VueCompareImage,
  },
  data() {
    return {
      code1,
      code2,
      code3,
      code4,
    };
  },
});
</script>

<style lang="scss">
body {
  margin: 0;
}
</style>

<style scoped lang="scss">
.container {
  background: gray;
}
pre {
  margin-top: 8rem;
  &:first-of-type {
    margin-top: 0;
  }
}
</style>
