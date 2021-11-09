# youtube project

- process.env 사용
- vue animation 추가
- vue bootstarp 추가 

## youtube Data API

- API KEY 보안을 위해 process.env 사용
- video 에서 필요한 정보만 가져오기

```js
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
		// video 에서 필요한 정보만 가져오기
      this.videos = videos.map((video) => {
        const { snippet } = video;

        return {
          videoId: video.id.videoId,
          title: _.unescape(snippet.title),
          description: _.unescape(snippet.description),
          thumbnailsUrl: snippet.thumbnails.default.url,
        };
      });
    },
```

## vue animation 추가 

### VideoList

```vue
<template>
  <div class="mb-5">
    <b-list-group>
      <transition-group name="list" tag="ul"
        ><video-list-item
          v-for="video in videos"
          :key="video.title"
          :video="video"
          class="shadow"
          @select-video="onSelectVideo"
        ></video-list-item
      ></transition-group>
    </b-list-group>
  </div>
</template>

//////////////////////////

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}

.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
```

### VideoDetail

```vue
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

/////////////////////////////

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
```

- App.vue

  선택된 비디오가 갑자기 나타나지 않도록 설정

  ```vue
      onSelectVideo(video) {
        this.video = null;
        setTimeout(() => {
          this.video = video;
        }, 100);
      },
  ```

  
