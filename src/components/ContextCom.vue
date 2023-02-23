<template>
  <div class="context">
    <h1>Your videos</h1>

    <form action="">
      <div class="form-group">
        <input
          type="checkbox"
          @change="changeOrder"
          :checked="rules.reverse"
          name="reverse"
          id="reverse"
        />
        <label for="reverse"> Reverse</label>
      </div>
      <div class="form-group">
        <input
          type="checkbox"
          @change="changeOrder"
          :checked="rules.byId"
          name="byId"
          id="byId"
        />
        <label for="reverse"> Order By Id</label>
      </div>
      <div class="form-group">
        <input
          type="checkbox"
          @change="changeOrder"
          :checked="rules.byName"
          name="byName"
          id="byName"
        />
        <label for="reverse"> Order By Name</label>
      </div>
    </form>
    <table class="table" border="1">
      <tr class="table-headRow">
        <th class="table-headCell">Id</th>
        <th class="table-headCell">Name</th>
        <th class="table-headCell">URL</th>
        <th class="table-headCell">Delete</th>
      </tr>
      <tr class="table-row" v-for="video in videos" :key="video.url">
        <td class="table-cell">#{{ video.id }}</td>
        <td class="table-cell">{{ video.name }}</td>
        <td class="table-cell">{{ video.url }}</td>
        <td class="table-cell" @click="deleteVideo(video)">X</td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  props: {
    videos: {
      type: Array,
      required: true,
    },
    rules: {
      type: Object,
      required: true,
      default() {
        return {};
      },
    },
  },
  methods: {
    deleteVideo(video) {
      this.$emit("deleteV", video);
    },
    changeOrder($event) {
      this.$emit("changeOrder", {
        name: $event.target.name,
        checked: $event.target.checked,
      });
    },
  },
};
</script>
<style scoped lang="scss">
.context {
  h1 {
    text-align: center;
  }

  form {
    display: flex;
    align-content: center;
    justify-content: center;
    align-items: center;
    background: palegoldenrod;
    padding: 0.9rem;
    width: 50%;
    margin-left: 22rem;
    border-radius: 10px;

    .form-group {
      margin-right: 10%;
    }
  }
  .table {
    margin: 2% 10px 5px 10%;
    width: 80%;
    border-collapse: separate;
  }

  .table-headRow,
  .table-row {
    text-align: left;
  }

  .table-headRow {
    background: #e5e5e5;
    .table-headCell,
    .table-cell {
      padding: 0.4rem;
    }
    .table-cell:last-child {
      color: tomato;
      text-align: center;
      font-weight: bold;
      cursor: pointer;
    }
  }
}
</style>
