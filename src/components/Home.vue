<template>
  <div class="home">
    <Counter />
  </div>
</template>

<script>
import Counter from "@/components/Counter.vue";

export default {
  name: "Home",
  components: {
    Counter,
  },
};
</script>

<style scoped>
.home {
  justify-content: center;
  display: flex;
  align-items: center;
}
</style>
