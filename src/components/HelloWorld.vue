<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Text box expand sample</h3>
    <input ref="rp-input" class="rp-input" v-model="text">
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      text: "",
      factor: 7.7,
      constantSideWidth: 20,
      canvas: document.createElement("canvas"),
      font: null,
      typingSpeed: 20
    };
  },
  watch: {
    text(newVal, oldVal) {
      this.typingSpeed = (this.getTextLength(newVal, this.font) - this.getTextLength(oldVal, this.font))
      this.resize();
    }
  },
  mounted () {
    this.font = getComputedStyle(this.$refs["rp-input"])['font']
    console.log('font', this.font)
  },
  methods: {
    resize() {
      let el = this.$refs["rp-input"];
      // const newWidth = (this.text.length + 1) * this.factor;
      let newWidth = this.getTextLength(this.text, this.font) + this.constantSideWidth;
      if (this.typingSpeed > 7.8) {
        newWidth += this.typingSpeed * 10.5
      }
      el.style.width = newWidth + "px";
      console.log('typing speed', this.typingSpeed)
      this.typingSpeed = 0
      // console.log(this.$refs["rp-input"]);
      // console.log(this.$refs["rp-input"].style['font'])
      // console.log(getComputedStyle(this.$refs["rp-input"])['font'])
      // let font = getComputedStyle(this.$refs["rp-input"])['font']
      // console.log(this.getTextLength(this.text, this.font))
    },
    getTextLength(text, font) {
      let context = this.canvas.getContext("2d");
      context.font = font;
      const metrics = context.measureText(text);
      return metrics.width;
    }

// console.log(getTextWidth("hello there!", "bold 12pt arial"));
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  text-align: center;
  padding: 20px;
}
.rp-input {
  width: 50px;
  min-width: 50px !important;
  max-width: 99.99% !important;
  transition: width 0.25s;
  text-align: left;
  border: 0px;
  border-bottom: 1px dashed;
  height: 30px;
  font-size: 14px;
}
.rp-input:focus {
  outline: none;
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
