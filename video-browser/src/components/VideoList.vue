<template>
  <ul class="list-group col-md-4">
    <VideoListItem
      v-for="video in videos"
      :video="video"
      :key="video.etag"
      @videoSelect="onVideoSelect"
    ></VideoListItem>
    <!-- ^This is passing each video as props to videolistitem -->
  </ul>
</template>

<script>
import VideoListItem from "./VideoListItem";
export default {
  name: "VideoList",
  components: {
    VideoListItem
  },
  methods: {
    onVideoSelect(video) {
      this.$emit("videoSelect", video);
    }
  },
  props: ["videos"] // <-- How you pass similar to props.videos in react, specify object for typechecking or array versions accessed just with the name no props.videos or this.props.videos
};
</script>

<style>
</style>
