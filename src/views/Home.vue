<script>
import { ref, watch } from 'vue';

import ComponentOne from '@/components/ComponentOne.vue';
import ComponentTwo from '@/components/ComponentTwo.vue';

export default {
  components: { ComponentOne, ComponentTwo },
  setup() {
    const componentOneRef = ref(null);

    watch(componentOneRef, () => console.log(componentOneRef.value.obj.name));

    return { componentOneRef };
  },
};
</script>

<template>
  <ComponentOne ref="componentOneRef">
    <ComponentTwo />
  </ComponentOne>
</template>

<style></style>
