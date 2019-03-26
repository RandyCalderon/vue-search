<template>
  <div>
    <!-- Binding the emission for search change -->
    <SearchBar @termChange="onTermChange"></SearchBar>
    <!-- Shorthand for v-bind: -->
    <VideoList :videos="videos"></VideoList>
    {{videos.length}}
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";

const API_KEY = "AIzaSyBB2KxL4VrzgQWmjpq1C8qHvGMWI4IP0Pg";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data: function() {
    return { videos: [] };
  },
  methods: {
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
