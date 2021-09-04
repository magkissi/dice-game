<template>
  <div class="btn-container">
    <button @click="onClick">{{ pic }} {{ text }}</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    pic: String,
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>

<style scoped>
.btn-container {
  display: flex;
}
button {
  width: auto;
  font-size: 20px;
  border-radius: 25px;
  border-style: none;
  height: 50px;
  cursor: pointer;
  padding-left: 15px;
  padding-right: 15px;
  color: rgb(83, 81, 81);
}
</style>
