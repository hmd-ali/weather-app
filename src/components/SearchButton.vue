<template>
  <button>{{ text }}</button>
</template>

<script>
export default {
  name: "SearchButton",
  props: {
    text: String,
  },
};
</script>

<style scoped>
button {
  padding: 1rem 1rem;
  background: #6e707a;
  color: #e7e7eb;
  border: none;
  border-radius: 1rem;
  font-size: 2rem;
}
button:hover {
  background: #e7e7eb;
  color: #111111;
  cursor: pointer;
}
</style>