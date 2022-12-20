<template>
  <div class="headerComponent">
    <h1>{{ mainTitle }}</h1>
    <h2>{{ tagline }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    mainTitle: String,
    tagline: String,
  },
};
</script>

<style scoped>
.headerComponent {
  display: flex;
  flex-direction: column;
  text-align: center;
}
</style>
