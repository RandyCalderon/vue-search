<template>
  <div>
    <!-- Binding the emission for search change -->
    <SearchBar @termChange="onTermChange"></SearchBar>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";

const API_KEY = "AIzaSyBB2KxL4VrzgQWmjpq1C8qHvGMWI4IP0Pg";

export default {
  name: "App",
  components: {
    SearchBar
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
        .then(response => console.log(response));
    }
  }
};
</script>
