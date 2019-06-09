<template>
  <div>
    <div id="on" @click="onSwitch(true)" :class="{ active: value }">
      On
    </div>
    <div id="off" @click="onSwitch(false)" :class="{ active: !value }">
      Off
    </div>
  </div>
</template>

<script>
export default {
  props: ["value"],
  methods: {
    onSwitch(boolValue) {
      this.$emit("input", boolValue);
    }
  }
};
</script>

<style scoped>
#on,
#off {
  width: 40px;
  height: 20px;
  background-color: lightgray;
  padding: 2px;
  display: inline-block;
  margin: 10px -2px;
  box-sizing: content-box;
  cursor: pointer;
  text-align: center;
}
#on:hover,
#on.active {
  background-color: green;
  color: white;
}
#off:hover,
#off.active {
  background-color: red;
  color: white;
}
</style>
