<template>
  <button v-bind:class="[tempStatus ? 'active' : '']" @click="onClick()">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "TempButton",
  props: {
    text: String,
    tempStatus: Boolean,
  },
  emits:['temp-btn-click'],
  methods: {
    onClick() {
      this.$emit("temp-btn-click");
    },
  },

};
</script>

<style scoped>
button {
  background: #585676;
  color: #e7e7eb;
  font-size: 1.6rem;
  font-weight: 500;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  border: none;
  padding: 0.5rem;
  margin: 1rem;
  cursor: pointer;
}
button.active {
  background: #e7e7eb;
  color: #110e3c;
}
</style>