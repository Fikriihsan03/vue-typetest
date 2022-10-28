<template>
  <div>
    <h1>VUE TYPING TEST</h1>
    <div class="parameter-wrapper">
      <p>Mistakes {{ mistakes }}</p>
      <p>
        Accuracy
        {{
            100 - ((+mistakes / +inputtedIndex) * 100).toFixed(2)
        }}%
      </p>
      <p>char {{ inputtedIndex }}</p>
      <p>Words {{ countWords }}</p>
      <p>WPM {{ inputtedIndex / 5 }}</p>
    </div>

    <div :class="!isTyping ? 'blur' : null">
      <div class="isTypingWrap" tabindex="0" @keydown="keyhandler" ref="isTypingWrap">
        <span class="initial" :class="getLetterColor(index)" :key="index" v-for="(item, index) in paragraph">{{ item
        }}</span>
      </div>
    </div>
    <div v-if="!isTyping"
      style="display: flex; justify-content: center; align-items: center;margin-top: 50px;margin-bottom:50px">
      <div style="width: 20%">
        <button @click="focusToTyping" class="button-19" role="button">click here to start</button>
      </div>
    </div>
  </div>
</template>

<script>
import { article } from "txtgen";
export default {
  name: "HomeView",
  data() {
    return {
      paragraph: [],
      text: "",
      inputtedIndex: 0,
      mistakes: 0,
      inputtedText: [],
      countWords: 0,
      isTyping: false,
    };
  },
  props: {
    msg: String,
  },
  mounted() {
    this.paragraph = article(2)
      .toLocaleLowerCase()
      .replace(/[^a-zA-Z0-9 ]/g, "")
      .split("");
  },
  methods: {
    keyhandler(event) {
      if (event.key !== this.paragraph[this.inputtedIndex]) {
        this.mistakes++;
      }
      if (event.key === "Backspace") {
        this.inputtedIndex--;
        this.mistakes--;
        this.inputtedText = this.inputtedText.slice(0, -1)
      } else {

        if (event.key === " ") {
          this.countWords++;
        }
        this.inputtedText.push(event.key);
        this.inputtedIndex++;
      }
    },

    getLetterColor(index) {
      switch (true) {
        case index === this.inputtedIndex:
          return "border-yellow"
        case this.paragraph[index] === this.inputtedText[index]:
          return "green"
        case index < this.inputtedIndex && this.paragraph[index] !== this.inputtedIndex[index]:
          return "red"

        default:
          ''
      }
    },

    focusToTyping() {
      this.isTyping = true;
      this.$refs.isTypingWrap.focus();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.initial {
  color: grey;
  border-left: transparent 2px solid;
}

.red {
  color: red !important;
}

.blur {
  cursor: pointer;
  filter: blur(8px);
}

.border-yellow {
  border-left: yellow 2px solid !important;
}

.green {
  color: green !important;
  /* display: none; */
}

.parameter-wrapper {
  display: flex;
  justify-content: center;
  gap: 50px;
}

.isTypingWrap {
  line-height: 50px;
  font-size: 1.5rem;
  height: 156.75px;
  overflow: hidden;
  user-select: none;
  width: 100%;
  margin-left: unset;
  transition: all 0.25s ease 0s;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

/* CSS */
.button-19 {
  appearance: button;
  background-color: #1899d6;
  border: solid transparent;
  border-radius: 16px;
  border-width: 0 0 4px;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-block;
  font-family: din-round, sans-serif;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.8px;
  line-height: 20px;
  margin: 0;
  outline: none;
  overflow: visible;
  padding: 13px 16px;
  text-align: center;
  text-transform: uppercase;
  touch-action: manipulation;
  transform: translateZ(0);
  transition: filter 0.2s;
  user-select: none;
  -webkit-user-select: none;
  vertical-align: middle;
  white-space: nowrap;
  width: 100%;
}

.button-19:after {
  background-clip: padding-box;
  background-color: #1cb0f6;
  border: solid transparent;
  border-radius: 16px;
  border-width: 0 0 4px;
  bottom: -4px;
  content: "";
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  z-index: -1;
}

.button-19:main,
.button-19:focus {
  user-select: auto;
}

.button-19:hover:not(:disabled) {
  filter: brightness(1.1);
  -webkit-filter: brightness(1.1);
}

.button-19:disabled {
  cursor: auto;
}
</style>
