<template>
  <div class="container">
    <!-- Binding the emission for search change -->
    <SearchBar @termChange="onTermChange"></SearchBar>
    <!-- Shorthand for v-bind: -->
    <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";

const API_KEY = "AIzaSyD9nygHgmyz99ZEAo6B5tTMhloHRIjLIVk";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return { videos: [] };
  },
  methods: {
    onVideoSelect(video) {
      console.log(video);
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
          this.videos = response.data.items;
        });
    }
  }
};
</script>
