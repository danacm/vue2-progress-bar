<!--
 * @Date: 2020-07-13 20:44:05
 * @Author: dana_chen@sina.cn
 * @LastEditors: dana_chen@sina.cn
 * @LastEditTime: 2020-07-13 22:17:20
-->
<template>
  <div class="page">
    <h1>Vue.js Linear Progress Bar</h1>
    <p class="spc-b">Linear progress bar component with gradients and animations!</p>
    <div class="spc-b">
      <div class="widget">
        <a
          class="btn git-txt"
          href="https://github.com/danacm/vue2-progress-bar"
          rel="noopener"
          target="_blank"
          aria-label="Star danacm/vue2-progress-bar on GitHub"
        >
          <svg
            viewBox="0 0 16 16"
            width="14"
            height="14"
            class="octicon octicon-mark-github"
            aria-hidden="true"
          >
            <path
              fill-rule="evenodd"
              d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"
            />
          </svg>
          <span class="txt">View on Github</span>
        </a>
      </div>
    </div>
    <div id="app">
      <div class="progress-display">
        <progress-bar
          :height="height"
          :width="width"
          :total-steps="totalSteps"
          :completed-steps="completedSteps"
          :animate-speed="animateSpeed"
          :stroke-linecap="strokeLinecap"
          :start-color="startColor"
          :stop-color="stopColor"
          :inner-stroke-color="innerStrokeColor"
          :timing-func="timingFunc"
          :show-tip="showTip"
        ></progress-bar>
        <div class="controls">
          <button :disabled="completedSteps <= 0" @click.prevent="prevStep">Prev</button>
          <button :disabled="completedSteps >= totalSteps" @click.prevent="nextStep">Next</button>
        </div>
      </div>
      <table class="progress-controls text-right">
        <tr>
          <td>
            <label for="height">height</label>
          </td>
          <td>
            <input
              id="height"
              type="number"
              placeholder="height"
              :value="height"
              @input="heightChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="width">width</label>
          </td>
          <td>
            <input
              id="width"
              type="number"
              placeholder="width"
              :value="width"
              @input="widthChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="total-steps">Total steps</label>
          </td>
          <td>
            <input
              id="total-steps"
              type="number"
              placeholder="Total steps"
              :value="totalSteps"
              @input="totalStepsChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="animate-speed">Animate speed</label>
          </td>
          <td>
            <input
              id="animate-speed"
              type="number"
              placeholder="Animate speed"
              :value="animateSpeed"
              @input="animateSpeedChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="timing-function">Timing function</label>
          </td>
          <td>
            <input
              id="timing-function"
              type="text"
              placeholder="Timing function"
              :value="timingFunc"
              @input="timingFuncChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="start-color">Start color</label>
          </td>
          <td>
            <input
              id="start-color"
              type="color"
              placeholder="Start color"
              :value="startColor"
              @input="startColorChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="stop-color">Stop color</label>
          </td>
          <td>
            <input
              id="stop-color"
              type="color"
              placeholder="Stop color"
              :value="stopColor"
              @input="stopColorChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="inner-stroke-color">Inner stroke color</label>
          </td>
          <td>
            <input
              id="inner-stroke-color"
              type="color"
              placeholder="Inner stroke color"
              :value="innerStrokeColor"
              @input="innerStrokeColorChanged"
            />
          </td>
        </tr>
        <tr>
          <td>
            <label for="showTip">showTip</label>
          </td>
          <td>
            <input id="showTip" type="checkbox" :checked="showTip" @input="showTipChanged" />
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
// import ProgressBar from "./components/ProgressBar.vue";
import ProgressBar from "vue2-progress-bar";

export default {
  name: "App",
  components: {
    ProgressBar
  },
  data() {
    return {
      completedSteps: 1,
      totalSteps: 10,
      animateSpeed: 1000,
      height: 50,
      width: 800,
      showTip: true,
      strokeLinecap: "round",
      startColor: "#bbff42",
      stopColor: "#0413dc",
      innerStrokeColor: "#d6efff",
      timingFunc: "linear"
    };
  },
  methods: {
    showTipChanged(e) {
      this.showTip = e.target.checked;
    },
    timingFuncChanged(e) {
      this.timingFunc = e.target.value;
    },

    innerStrokeColorChanged(e) {
      this.innerStrokeColor = e.target.value;
    },

    stopColorChanged(e) {
      this.stopColor = e.target.value;
    },

    startColorChanged(e) {
      this.startColor = e.target.value;
    },

    widthChanged(e) {
      e.preventDefault();
      const val = e.target.value;

      if (!val || isNaN(val)) {
        return false;
      }

      this.width = parseInt(val);
    },

    heightChanged(e) {
      e.preventDefault();
      const val = e.target.value;

      if (!val || isNaN(val)) {
        return false;
      }

      this.height = parseInt(val);
    },

    animateSpeedChanged(e) {
      e.preventDefault();
      const val = e.target.value;

      if (!val || isNaN(val)) {
        return false;
      }

      this.animateSpeed = parseInt(val);
    },

    totalStepsChanged(e) {
      e.preventDefault();
      const val = e.target.value;

      if (!val || isNaN(val)) {
        return false;
      }

      this.totalSteps = parseInt(val);
    },
    nextStep() {
      this.completedSteps += 1;
    },
    prevStep() {
      this.completedSteps -= 1;
    },
    startProgress() {
      const self = this;
      if (this.timer) {
        window.clearInterval(this.timer);
      }
      this.timer = setInterval(() => {
        if (self.completedSteps === self.totalSteps) {
          self.completedSteps = 0;
        } else {
          self.completedSteps++;
        }
      }, 1000);
    }
  },
  mounted() {
    // this.startProgress();
  }
};
</script>

<style>
html,
body {
  background: #4e4f4f;
  text-align: center;
  color: #fff;
  font-family: "Open Sans", Helvetica, Verdana, sans-serif;
  font-size: 16px;
}
#app {
  width: 100%;
  display: flex;
  align-items: center;
}

.progress-display {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.progress-controls {
  display: block;
  flex: 1;
}
.controls {
  margin-top: 10px;
  text-align: center;
}
.controls button {
  border-radius: 5px;
  color: #fff;
  padding: 13px 20px;
  background: #ff9f37;
  border: 0;
  outline: 0;
  line-height: 1.3em;
  text-transform: uppercase;
  cursor: pointer;
  box-sizing: border-box;
  margin-left: 10px;
}
.controls button:hover {
  background: #ff9f37;
}
p {
  margin: 5px 0;
}
.visible-collapse {
  visibility: collapse;
}
input {
  margin: 0;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
input,
button {
  font: inherit;
  margin-bottom: 10px;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
label {
  margin-right: 15px;
}
.spc-b {
  margin-bottom: 30px;
}
.widget {
  display: inline-block;
  overflow: hidden;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Helvetica, Arial,
    sans-serif;
  font-size: 0;
  line-height: 0;
  white-space: nowrap;
}
.btn {
  color: #24292e;
  background-color: #eff3f6;
}
.git-txt {
  position: relative;
  display: inline-block;
  height: 14px;
  padding: 3px 5px;
  font-size: 11px;
  font-weight: 600;
  line-height: 14px;
  vertical-align: bottom;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  background-repeat: repeat-x;
  background-position: -1px -1px;
  background-size: 110% 110%;
}
.txt {
  margin-left: 10px;
  position: relative;
  top: -3px;
}
</style>
