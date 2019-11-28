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
      factor: 7.7
    };
  },
  watch: {
    text(val) {
      this.resize();
    }
  },
  methods: {
    resize() {
      let el = this.$refs["rp-input"];
      const newWidth = (this.text.length + 1) * this.factor;
      // if (newWidth > 50)
      el.style.width = newWidth + "px";
      console.log(this.$refs["rp-input"]);
    }
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
