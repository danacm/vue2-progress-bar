<template>
  <div class="progress-container" :style="containerStyle">
    <div :style="innerBlockStyle">
      <slot name="header"></slot>
    </div>
    <div class="svg-content">
      <svg
        class="progress-bar"
        :viewBox="viewBox"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
      >
        <defs>
          <linearGradient
            :id="'gradient' + _uid"
            :x1="gradient.x1"
            :y1="gradient.y1"
            :x2="gradient.x2"
            :y2="gradient.y2"
            gradientUnits="userSpaceOnUse"
          >
            <stop offset="30%" :stop-color="startColor" />
            <stop offset="100%" :stop-color="stopColor" />
          </linearGradient>
        </defs>
        <line
          x1="5"
          y1="5"
          :x2="width"
          y2="5"
          fill="transparent"
          :stroke="innerStrokeColor"
          :stroke-dasharray="circumference"
          stroke-dashoffset="0"
          :stroke-linecap="strokeLinecap"
          :style="outerStyle"
        />
        <line
          x1="5"
          y1="5"
          :x2="width"
          y2="5"
          :stroke="'url(#gradient' + _uid + ')'"
          :stroke-dasharray="circumference"
          stroke-dashoffset="0"
          :stroke-linecap="strokeLinecap"
          :style="innerStyle"
        />
      </svg>
    </div>
    <div :style="innerBlockStyle">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProgressBar",
  props: {
    viewBox: {
      type: true,
      required: false,
      default: "0 0 210 10"
    },
    totalSteps: {
      type: Number,
      required: true,
      default: 10
    },
    completedSteps: {
      type: Number,
      required: true,
      default: 0
    },
    startColor: {
      type: String,
      required: false,
      default: "#73cbfe"
    },
    stopColor: {
      type: String,
      required: false,
      default: "#458efd"
    },
    outerStrokeWidth: {
      type: Number,
      required: false,
      default: 10
    },
    innerStrokeWidth: {
      type: Number,
      required: false,
      default: 10
    },
    strokeLinecap: {
      type: String,
      required: false,
      default: "round"
    },
    animateSpeed: {
      type: Number,
      required: false,
      default: 1000
    },
    timingFunc: {
      type: String,
      required: false,
      default: "linear"
    },
    innerStrokeColor: {
      type: String,
      required: false,
      default: "#d6efff"
    }
  },

  data() {
    return {
      gradient: {
        x1: 0,
        x2: this.width,
        y1: 0,
        y2: 0
      },
      gradientAnimation: null,
      currentAngle: 0,
      strokeDashoffset: this.width,
      width: 200,
      height: 10,
      containerWidth: 200
    };
  },

  computed: {
    circumference() {
      return this.width;
    },
    outerStyle() {
      return {
        height: `${this.height}px`,
        width: `${this.width}px`,
        strokeWidth: `${this.outerStrokeWidth}px`
      };
    },
    innerStyle() {
      return {
        height: `${this.height}px`,
        width: `${this.width}px`,
        strokeWidth: `${this.innerStrokeWidth}px`,
        strokeDashoffset: this.strokeDashoffset,
        transition: `stroke-dashoffset ${this.animateSpeed}ms ${this.timingFunc}`
      };
    },
    innerBlockStyle() {
      return {
        width: `${this.containerWidth}px`
      };
    },
    containerStyle() {
      return {
        width: `${this.containerWidth}px`
      };
    },
    innerWith() {
      return (this.completedSteps / (this.totalSteps)) * this.width;
    }
  },

  methods: {
    gotoGradientPoint() {
      this.gradient.x2 = this.innerWith;
    },
    changeProgress() {
      this.strokeDashoffset = this.width - this.innerWith;
    }
  },

  watch: {
    totalSteps() {
      this.changeProgress();
    },

    completedSteps() {
      this.changeProgress();
    }
  },

  created() {
    const self = this;
    self.changeProgress();
    self.$nextTick(() => {
      self.containerWidth = document.getElementsByClassName(
        "progress-container"
      )[0].offsetWidth;
    });
  }
};
</script>

<style>
.progress-container {
  position: relative;
}
</style>
