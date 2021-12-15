<script>
import { ref } from 'vue';

import VideoJS from '@/components/VideoJS.vue';

export default {
  components: { VideoJS },
  setup() {
    const VideoJSRef = ref(null);

    const fullScreenChange = () => console.log('fullScreenChange!!!');

    return { VideoJSRef, fullScreenChange };
  },
};
</script>

<template>
  <VideoJS ref="VideoJSRef" @vpFullScreenChange="fullScreenChange" />
</template>

<style></style>
