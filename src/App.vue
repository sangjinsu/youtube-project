<template>
  <div id="app">
    <b-container>
      <header>
        <h1 class="fw-bold">My first youtube project</h1>
        <the-search-bar @search-keyword="onSearchKeyword"></the-search-bar>
      </header>
      <video-detail :video="video"></video-detail>
      <video-list :videos="videos" @select-video="onSelectVideo"></video-list
    ></b-container>
  </div>
</template>

<script>
import TheSearchBar from "@/components/TheSearchBar";
import VideoList from "@/components/VideoList";
import VideoDetail from "@/components/VideoDetail";
import axios from "axios";
import _ from "lodash";

export default {
  name: "App",
  components: {
    TheSearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return {
      keyword: null,
      videos: null,
      video: null,
    };
  },
  methods: {
    async onSearchKeyword(keyword) {
      this.keyword = keyword;

      const params = {
        key: process.env.VUE_APP_API_KEY,
        part: "snippet",
        type: "video",
        q: this.keyword,
      };

      const {
        data: { items: videos },
      } = await axios({
        method: "get",
        url: process.env.VUE_APP_API_URL,
        params,
      }).catch((err) => {
        console.log(err);
      });

      const timeout = 800;

      setTimeout(() => {
        this.videos = videos.map((video) => {
          const { snippet } = video;

          return {
            videoId: video.id.videoId,
            title: _.unescape(snippet.title),
            description: _.unescape(snippet.description),
            thumbnailsUrl: snippet.thumbnails.default.url,
          };
        });
      }, timeout);
    },

    onSelectVideo(video) {
      this.video = null;
      setTimeout(() => {
        this.video = video;
      }, 100);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
