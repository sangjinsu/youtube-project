<template>
  <b-list-group-item @click="selectVideo" class="d-flex justify-content-center">
    <b-img
      thumbnail
      fluid
      :src="video.thumbnailsUrl"
      alt="youtube-thumbnail-image"
    />
    <p class="text-break text-center">{{ video.title }}</p>
  </b-list-group-item>
</template>

<script>
export default {
  name: "VideoListItem",
  props: {
    video: {
      type: Object,
      required: true,
    },
  },
  methods: {
    selectVideo() {
      this.$emit("select-video", this.video);
    },
  },
};
</script>