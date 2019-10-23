<template>
  <div class="vci-container" ref="containerRef">
    <img
      :alt="leftImageAlt"
      :src="leftImage"
      :style="leftImageStyle"
      class="left-image"
      ref="leftImageRef"
    />
    <div :style="leftImageStyle" class="left-label">{{leftLabel}}</div>

    <img :alt="rightImageAlt" :src="rightImage" class="right-image" ref="rightImageRef" />
    <div :style="rightLabelStyle" ref="rightLabelRef" class="right-label">{{rightLabel}}</div>

    <div :style="sliderStyle" class="vci-slider">
      <div :style="sliderLineStyle" class="line" />
      <div :style="sliderHandleStyle" class="handle">
        <div :style="sliderLeftArrowStyle" class="left-arrow" />
        <div :style="sliderRightArrowStyle" class="right-arrow" />
      </div>
      <div :style="sliderLineStyle" class="line" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import { ResizeSensor } from 'css-element-queries';

export default Vue.extend({
  mounted() {
    // get and set `imageWidth` when the container size changed
    // (including first time rendering)
    //
    // eslint-disable-next-line
    new ResizeSensor(this.$refs.containerRef, () => {
      this.getAndSetImageWidth();
    });

    const containerElement = this.$refs.containerRef;

    // for mobile
    containerElement.addEventListener('touchstart', this.startSliding);
    window.addEventListener('touchend', this.finishSliding);

    // for desktop
    if (this.hover) {
      containerElement.addEventListener('mouseenter', this.startSliding);
      containerElement.addEventListener('mouseleave', this.finishSliding);
    } else {
      containerElement.addEventListener('mousedown', this.startSliding);
      window.addEventListener('mouseup', this.finishSliding);
    }
  },
  beforeDestroy() {
    this.finishSliding();
    window.removeEventListener('mouseup', this.finishSliding);
    window.removeEventListener('touchend', this.finishSliding);
  },
  props: {
    leftImage: {
      type: String,
      default: '',
    },
    leftImageAlt: {
      type: String,
      default: null,
    },
    leftLabel: {
      type: String,
      default: '',
    },
    // under image
    rightImage: {
      type: String,
      default: '',
    },
    rightImageAlt: {
      type: String,
      default: null,
    },
    rightLabel: {
      type: String,
      default: '',
    },
    hover: {
      type: Boolean,
      default: false,
    },
    handleSize: {
      type: Number,
      default: 40,
    },
    sliderLineWidth: {
      type: Number,
      default: 2,
    },
    sliderPositionPercentage: {
      type: Number,
      default: 0.5,
    },
  },
  methods: {
    getAndSetImageWidth() {
      // @ts-ignore
      this.imageWidth = this.$refs.rightImageRef.getBoundingClientRect().width;
      this.rightLabelWidth = this.$refs.rightLabelRef.getBoundingClientRect().width;
    },
    startSliding(e) {
      // Prevent default behavior other than mobile scrolling
      if (!('touches' in e)) {
        e.preventDefault();
      }

      // Slide the image even if you just click or tap (not drag)
      this.updateSliderPosition(e);

      window.addEventListener('mousemove', this.updateSliderPosition);
      window.addEventListener('touchmove', this.updateSliderPosition);
    },
    finishSliding() {
      window.removeEventListener('mousemove', this.updateSliderPosition);
      window.removeEventListener('touchmove', this.updateSliderPosition);
    },
    updateSliderPosition(event) {
      const e = event || window.event;

      // Calc Cursor Position from the left edge of the viewport
      const cursorXfromViewport = e.touches ? e.touches[0].pageX : e.pageX;

      // Calc Cursor Position from the left edge of the window (consider any page scrolling)
      const cursorXfromWindow = cursorXfromViewport - window.pageXOffset;

      // Calc Cursor Position from the left edge of the image
      const imagePosition = this.$refs.rightImageRef.getBoundingClientRect();
      let pos = cursorXfromWindow - imagePosition.left;

      // Set minimum and maximum values ​​to prevent the slider from overflowing
      const minPos = 0 + this.sliderLineWidth / 2;
      const maxPos = this.imageWidth - this.sliderLineWidth / 2;

      if (pos < minPos) pos = minPos;
      if (pos > maxPos) pos = maxPos;

      this.positionPct = pos / this.imageWidth;
    },
  },
  data() {
    return {
      // slider position percentage(0 to 1)
      positionPct: this.sliderPositionPercentage || 0.5,
      imageWidth: 0,
    };
  },
  computed: {
    // eslint-disable
    leftImageStyle() {
      return {
        clip: `rect(auto, ${this.imageWidth * this.positionPct}px, auto, auto)`,
      };
    },
    rightLabelStyle() {
      const cutLeft = Math.max(
        0,
        this.rightLabelWidth + this.imageWidth * (this.positionPct - 1),
      );
      return {
        clip: `rect(auto, auto, auto, ${cutLeft}px)`,
      };
    },
    sliderStyle() {
      return {
        cursor: !this.hover && 'ew-resize',
        left: this.imageWidth * this.positionPct - this.handleSize / 2 + 'px',
        width: `${this.handleSize}px`,
      };
    },
    sliderLineStyle() {
      return { width: `${this.sliderLineWidth}px` };
    },
    sliderHandleStyle() {
      return {
        border: `${this.sliderLineWidth}px solid white`,
        height: `${this.handleSize}px`,
        width: `${this.handleSize}px`,
      };
    },
    sliderLeftArrowStyle() {
      return {
        border: `inset ${this.handleSize * 0.15}px rgba(0,0,0,0)`,
        borderRight: `${this.handleSize * 0.15}px solid white`,
        marginLeft: `-${this.handleSize * 0.25}px`, // for IE11
        marginRight: `${this.handleSize * 0.25}px`,
      };
    },
    sliderRightArrowStyle() {
      return {
        border: `inset ${this.handleSize * 0.15}px rgba(0,0,0,0)`,
        borderLeft: `${this.handleSize * 0.15}px solid white`,
        marginRight: `-${this.handleSize * 0.25}px`, // for IE11
      };
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.vci-container {
  box-sizing: border-box;
  position: relative;
  width: 100%;
  overflow: hidden;
}

.left-image {
  display: block;
  height: 100%; // fit to the height of under image
  object-fit: cover; // protrudes is hidden
  position: absolute;
  top: 0;
  width: 100%;
}

.left-label {
  position: absolute;
  top: 0px;
  left: 0px;
  padding: 10px;
}

.right-image {
  display: block;
  height: auto; // Respect the aspect ratio
  width: 100%;
}

.right-label {
  position: absolute;
  top: 0px;
  right: 0px;
  padding: 10px;
}

.vci-slider {
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  position: absolute;
  top: 0;

  .line {
    background: white;
    box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2),
      0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
    flex: 0 1 auto;
    height: 100%;
  }

  .handle {
    align-items: center;
    border-radius: 100%;
    box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2),
      0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
    box-sizing: border-box;
    display: flex;
    flex: 1 0 auto;
    justify-content: center;
  }

  .left-arrow {
    height: '0px';
    width: '0px';
  }

  .right-arrow {
    height: '0px';
    width: '0px';
  }
}
</style>
