<script>
import { ref, reactive } from 'vue';

export default {
  setup() {
    const num = ref(69);

    const obj = reactive({
      name: 'Jun',
      age: 18,
    });

    return { num, obj };
  },
};
</script>

<template>
  <h1>Component One</h1>
  <slot />
</template>

<style></style>
