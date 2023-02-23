<template>
  <form class="form">
    <div class="form-group">
      <label class="form-label" for="url">Video Url: </label>
      <input v-model="videoUrl" class="form-input" type="url" id="url" />
    </div>

    <div class="form-group">
      <label class="form-label" for="name">Video name: </label>
      <input v-model="videoName" class="form-input" type="text" id="name" />
    </div>
    <button class="form-button" @click="addVideo">Add Video</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      videoUrl: "",
      videoName: "",
    };
  },
  methods: {
    addVideo($event) {
      $event.preventDefault();

      this.$emit("addMyVideo", {
        url: this.videoUrl,
        name: this.videoName,
      });
    },
  },
};
</script>
<style scoped lang="scss">
form {
  background: linear-gradient(80deg, lightblue, lightyellow);
  padding: 2% 0;
  width: 100%;

  margin-top: -60px;
  .form-group {
    display: flex;
    align-content: center;
    justify-content: center;
    align-items: center;
    padding: 1rem;
    .form-label {
      margin-right: 12px;

      font-size: 1.5rem;
    }
    .form-input {
      background: none;
      border: none;
      outline: none;
      border-bottom: 1px solid yellow;
      font-size: 1.5rem;
    }
  }
  .form-button {
    background-color: yellow;
    padding: 1%;
    margin: 1%;
    cursor: pointer;
  }
}
</style>
