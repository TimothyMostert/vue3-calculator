<template>
  <div class="home">
    <Calculator />
  </div>
</template>

<script>
import Calculator from "@/components/Calculator.vue";

export default {
  name: "Home",
  components: {
    Calculator,
  },
};
</script>

<style scoped lang="scss">
.home {
  display: flex;
  justify-content: center;
  padding: 2em;
}
</style>
