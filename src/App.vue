<template>
  <div>
    <Header-Com @addMyVideo="addMyVideo"></Header-Com>
    <!-- use $emit -->

    <Context-Com
      @changeOrder="changeOrder"
      :rules="rules"
      @deleteV="deleteV"
      :videos="displayedVideos"
    ></Context-Com>
    <!-- <Context-Com :videos="videos"></Context-Com> -->
  </div>
</template>

<script>
import ContextCom from "./components/ContextCom.vue";
import HeaderCom from "./components/HeaderCom.vue";
export default {
  name: "App",
  components: {
    ContextCom,
    HeaderCom,
  },
  data() {
    return {
      videos: [
        { id: 1, name: "Learn Vue", url: "http://vuejs.com" },
        { id: 2, name: "Learn Python", url: "http://Python.com" },
        { id: 3, name: "funny video", url: "http://funny.com" },
        { id: 4, name: "nice song", url: "http://songs.com" },
      ],
      rules: {
        reverse: false,
        byId: true,
        byName: false,
      },
    };
  },
  computed: {
    displayedVideos() {
      let final = [...this.AddiDToVideos];
      if (this.rules.byName) {
        final = this.sortByName;
      }
      if (this.rules.byId) {
        final = this.sortById;
      }
      return this.rules.reverse ? [...final].reverse() : final;
    },
    AddiDToVideos() {
      const result = [...this.videos].map((video, index) => ({
        ...video,
        id: video.id ? video.id : index + 1,
      }));
      return result;
    },
    sortById() {
      const result = [...this.AddiDToVideos].sort((a, b) => a.id - b.id);
      return result;
    },
    sortByName() {
      const result = [...this.AddiDToVideos].sort((a, b) => {
        const nameA = a.name.toLowerCase();
        const nameB = b.name.toLowerCase();
        if (nameA > nameB) return 1;
        if (nameA < nameB) return -1;
        return 0;
      });
      return result;
    },
  },
  methods: {
    addMyVideo(payload) {
      const { name, url } = payload;
      this.videos.push({
        name,
        url,
      });
    },
    deleteV(video) {
      console.log(video);
      this.videos = this.videos.filter(
        (v) => v.name !== video.name && v.url !== video.url
      );
    },
    changeOrder(payload) {
      const { name, checked } = payload;
      console.log(this.rules);
      this.rules[name] = checked;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
