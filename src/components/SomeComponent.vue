<template>
  <div class="some-component">
    Обычный компонент
    <slot />
  </div>
</template>

<script>
export default {
  name: "SomeComponent",
};
</script>

<style scoped lang="scss">
.some-component {
  border: 5px solid #8068be;
  margin: 10px;
  padding: 10px;
  font-size: 20px;
  color: #8068be;
  font-weight: 800;
}
</style>
