<template>
  <div class="mb-5">
    <b-list-group>
      <transition-group name="list" tag="ul">
        <video-list-item
          v-for="video in videos"
          :key="video.title"
          :video="video"
          class="shadow"
          @select-video="onSelectVideo"
        ></video-list-item>
      </transition-group>
    </b-list-group>
  </div>
</template>


<script>
import VideoListItem from "./VideoListItem.vue";

export default {
  name: "VideoList",
  components: {
    VideoListItem,
  },
  props: {
    videos: {
      type: Array,
    },
  },
  methods: {
    onSelectVideo(video) {
      this.$emit("select-video", video);
    },
  },
};
</script>

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.8s;
}

.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>