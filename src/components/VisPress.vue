<template>
  <div class="container1">
    <h1>{{ text }}</h1>
    <p class="text-data">
      <span>{{ Math.floor(data) }}</span> {{ units }}
    </p>
  </div>
</template>

<script>
export default {
  name: "VisPress",
  props: {
    text: String,
    units: String,
    data: Number,
  },
};
</script>

<style scoped>
.container1 {
  position: relative;
  width: 328px;
  height: 160px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  background: #1e213a;
  color: #e7e7eb;
}
h1 {
  font-size: 1.5rem;
  font-weight: 500;
}
.text-data {
  font-size: 3rem;
}
.text-data span {
  font-size: 5rem;
  font-weight: 700;
}
</style>