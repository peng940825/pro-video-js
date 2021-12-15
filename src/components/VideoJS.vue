<script>
import { ref, onMounted } from 'vue';

import 'video.js/dist/video-js.css';

import videojs from 'video.js';

export default {
  emits: ['vpFullScreenChange'],
  props: {
    addEventTypes: {
      type: Array,
      default: () => [],
    },
  },
  setup(props, { emit }) {
    let videoPlayer = null;

    let playPromise = null;

    const videoPlayerRef = ref(null);

    const videoPlayerOptions = {
      controls: true,
      controlBar: true,
      bigPlayButton: false,
    };

    const whenVideoPlayerReady = () => {
      // autoPlay();

      // videoPlayer.on('mouseenter', playVideo);
      // videoPlayer.on('mouseleave', pauseVideo);

      videoPlayer.on('canplay', () => console.log('canplay!!!'));
      videoPlayer.on('playing', () => console.log('playing!!!'));
      videoPlayer.on('pause', () => console.log('pause!!!'));
      videoPlayer.on('ended', () => console.log('ended!!!'));
      videoPlayer.on('error', () => console.log('error!!!'));
      videoPlayer.on('fullscreenchange', () => emit('vpFullScreenChange'));
    };

    const playVideo = () => {
      if (videoPlayer.currentSrc() === '') {
        // videoPlayer.src({
        //   type: 'video/mp4',
        //   src: 'https://firebasestorage.googleapis.com/v0/b/peng940825-2b6ec.appspot.com/o/IU.mp4?alt=media&token=f6c3bb39-b17f-4e15-8a6c-5349c442b511',
        // });

        videoPlayer.src({
          type: 'video/mp4',
          src: 'https://img.jvid.com/marked_preview_video/1627958989556_221840/2021/08/03/0c3456cd04b18d8291eb7c90d1edddc36154f9cdce13331721541c15b8c551d4.mp4',
        });
      }

      playPromise = videoPlayer.play();
    };

    const pauseVideo = () => playPromise.then(() => videoPlayer.pause());

    const autoPlay = () => {
      videoPlayer.src({
        type: 'video/mp4',
        src: 'https://img.jvid.com/marked_preview_video/1627958989556_221840/2021/08/03/0c3456cd04b18d8291eb7c90d1edddc36154f9cdce13331721541c15b8c551d4.mp4',
      });
      videoPlayer.volume(0);
      videoPlayer.loop(true);
      videoPlayer.muted(true);
      videoPlayer.autoplay(true);
      // videoPlayer.controls(false); // 不一定一定是 false
      videoPlayer.playsinline(true);
    };
    console.log(autoPlay);

    onMounted(() => {
      videoPlayer = videojs(
        videoPlayerRef.value,
        videoPlayerOptions,
        whenVideoPlayerReady
      );
    });

    return { videoPlayerRef, playVideo, pauseVideo };
  },
};
</script>

<template>
  <button type="buttom" @click="playVideo">Play</button>
  <button type="buttom" @click="pauseVideo">Pause</button>

  <!-- <a href="https:google.com" target="_blank"> -->
  <div class="video-container">
    <video
      ref="videoPlayerRef"
      class="video-js"
      preload="auto"
      poster="https://img.jvid.com/video_thumbnail/1616668080348_221840/2021/03/25/640/6783b876841c023acfaa041a4d290c22c62e330186c7acc3ee95835f04efa02f.jpg"
    ></video>
  </div>
  <!-- </a> -->
</template>

<style lang="scss" scoped>
.video-container {
  width: 600px;
  aspect-ratio: 3/2;

  .video-js {
    width: 100%;
    height: 100%;

    .vjs-tech {
      object-fit: cover;
    }

    /deep/ .vjs-poster {
      background-size: cover;
    }
  }
}
</style>
