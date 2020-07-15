<template>
  <div class="progress-container" :id="'container'+_uid" :style="containerStyle">
    <div :style="innerBlockStyle" v-if="$slots.header">
      <slot name="header"></slot>
    </div>
    <div class="svg-row">
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
            :x1="halfHight"
            :y1="halfHight"
            :x2="width"
            :y2="halfHight"
            fill="transparent"
            :stroke="innerStrokeColor"
            :stroke-dasharray="circumference"
            stroke-dashoffset="0"
            :stroke-linecap="strokeLinecap"
            :style="outerStyle"
          />
          <line
            :x1="halfHight"
            :y1="halfHight"
            :x2="width"
            :y2="halfHight"
            :stroke="'url(#gradient' + _uid + ')'"
            :stroke-dasharray="circumference"
            stroke-dashoffset="0"
            :stroke-linecap="strokeLinecap"
            :style="innerStyle"
          />
        </svg>
      </div>
      <div class="svg-tip" v-show="showTip">
        <span v-if="$slots.tip">
          <slot name="tip"></slot>
        </span>
        <span v-else>{{completedSteps}} / {{totalSteps}}</span>
      </div>
    </div>
    <div :style="innerBlockStyle" v-if="$slots.footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProgressBar",
  props: {
    height: {
      type: Number,
      default: 10
    },
    width: {
      type: Number,
      default: 200
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
    showTip: {
      type: Boolean,
      required: false,
      default: true
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
      viewBox: "",
      gradient: {
        x1: 0,
        x2: this.width,
        y1: 0,
        y2: 0
      },
      gradientAnimation: null,
      currentAngle: 0,
      strokeDashoffset: this.width,
      containerWidth: this.width
    };
  },

  computed: {
    outerStrokeWidth() {
      return this.height / 2;
    },
    innerStrokeWidth() {
      return this.height / 2;
    },
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
      return (this.completedSteps / this.totalSteps) * this.width;
    },
    halfHight() {
      return this.height / 2;
    }
  },

  methods: {
    gotoGradientPoint() {
      this.gradient.x2 = this.innerWith;
    },
    changeProgress() {
      if (this.strokeDashoffset < 0) {
        this.strokeDashoffset = this.width;
      } else {
        this.strokeDashoffset = this.width - this.innerWith;
      }
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
  mounted() {
    const self = this;
    self.viewBox = `0 0 ${parseInt(self.width) + 10} ${self.height}`;
    self.changeProgress();
  },
  created() {
    const self = this;
    self.$nextTick(() => {
      setTimeout(() => {
        const offWid = document.getElementById(`container${self._uid}`)
          .offsetWidth;
        self.containerWidth = offWid === self.width ? self.width : offWid;
      }, 1000);
    });
  }
};
</script>

<style lang="scss">
.progress-container {
  position: relative;
}
.svg-row {
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 100%;
  .svg-content {
    display: inline-block;
    width: 80%;
    margin-right: 2%;
  }
  .svg-tip {
    display: inline-block;
    width: 18%;
    font-size: 1em;
    text-align: left;
  }
}
</style>
