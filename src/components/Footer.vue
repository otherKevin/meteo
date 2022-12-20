<template>
  <div class="footerComponent">
    <p>{{ copyright }}</p>
    <p>Source : {{ links }}</p>
  </div>
</template>

<script>
export default {
  props: {
    copyright: String,
    links: String,
  },
};
</script>

<style scoped>
.footerComponent {
  display: flex;
  flex-direction: column;
  text-align: center;
}
</style>
