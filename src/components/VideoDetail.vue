<template>
  <transition name="detail">
    <div v-if="video" class="m-5">
      <iframe
        :src="videoURI"
        type="text/html"
        width="640"
        height="360"
        frameborder="0"
      ></iframe>
      <hr />
      <h4>{{ video.title }}</h4>
      <p class="text-break">{{ video.description }}</p>
      <hr />
    </div>
  </transition>
</template>

<script>
export default {
  name: "VideoDetail",

  props: {
    video: {
      type: Object,
    },
  },
  computed: {
    videoURI() {
      const { videoId } = this.video;
      return `https://youtube.com/embed/${videoId}`;
    },
  },
};
</script>

<style scoped>
.detail-enter-active,
.detail-leave-active {
  transition: all 1s;
}

.detail-enter,
.detail-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>