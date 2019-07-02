<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList></VideoList>
    {{ videos.length }}
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import { log } from "util";
const API_KEY = "AIzaSyDPkz4mVjkQ9JZaPyx1s4dSbjPpPcjApqs";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []
    };
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
        .then(({ data }) => (this.videos = data.items));
    }
  }
};
</script>