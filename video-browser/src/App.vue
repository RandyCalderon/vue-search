<template>
  <div class="container">
    <!-- Binding the vue emission for search change -->
    <SearchBar @termChange="onTermChange"></SearchBar>
    <!-- shorthand for v-bind shown here with :video-->
    <div class="row">
      <VideoDetail :video="selectedVideo"/>
      <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/Videodetail";

const API_KEY = "AIzaSyDRsMpny9Sbd88p5hnvqReB0cXXU9zoNfs";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return { videos: [], selectedVideo: null };
  },
  methods: {
    onVideoSelect(video) {
      console.log(video);
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm
          }
        })
        .then(response => {
          console.log(response);
          this.videos = response.data.items;
        });
    }
  }
};
</script>
