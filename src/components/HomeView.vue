<template>
  <div>
    <div>
      <p>Mistakes {{ mistakes }}</p>
      <p>
        Accuracy
        {{
          100 - ((Number(mistakes) / Number(inputtedIndex)) * 100).toFixed(2)
        }}%
      </p>
      <p>char {{ inputtedIndex }}</p>
      <p>WPM {{ inputtedIndex / 5 }}</p>
    </div>
    <div class="hello" tabindex="0" @keydown="keyhandler" ref="typingWrap">
      <span
        class="initial"
        :class="
          index === inputtedIndex
            ? 'border-yellow'
            : paragraph[index] === inputText[index]
            ? 'green'
            : index < inputtedIndex && paragraph[index] !== inputText[index]
            ? 'red'
            : 'initial'
        "
        :key="index"
        v-for="(item, index) in paragraph"
        >{{ item }}</span
      >
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
      inputText: [],
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
    this.$refs.typingWrap.focus();
  },
  methods: {
    keyhandler(event) {
      if (event.key !== this.paragraph[this.inputtedIndex]) {
        this.mistakes++;
      }
      if (event.key === "Backspace") {
        this.inputtedIndex--;
        this.mistakes--;
        return (this.inputText = this.inputText.slice(0, -1));
      }
      console.log(console.log(this.inputtedIndex));
      this.inputText.push(event.key);
      this.inputtedIndex++;
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
.border-yellow {
  border-left: yellow 2px solid !important;
}
.green {
  color: green !important;
  /* display: none; */
}
.hello {
  line-height: 50px;
  font-size: 1.5rem;
  height: 156.75px;
  overflow: hidden;
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
</style>
