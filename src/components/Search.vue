<template>
  <div class="content-header">
    <div class="search-container">
      <div class="child">
        <h3 class="search-bar-header">
          All Games <span>({{ contentLength }})</span>
        </h3>
        <input
          type="text"
          class="search-input"
          placeholder="Search Games"
          v-model="searchQuery"
          @change="search(searchQuery)"
        />
        <font-awesome-icon class="search-icon" icon="search" />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Search",
  props: ["contentLength"],
  data() {
    return {
      searchQuery: null
    };
  },
  methods: {
    search (searchQuery) {
      this.$emit('search-game', searchQuery)
    }
  }
};
</script>

<style scoped lang="scss">
.content-header {
  height: 85px;
  background-color: #494949;
  margin-top: 15px;
  width: 1290px;
}

.search-container {
  display: flex;
  flex-wrap: wrap;
  .child {
    flex: 1 0 21%;
    margin: 5px;
    height: 50px;
    padding: 10px 30px;
    position: relative;
    .search-bar-header {
      font-family: poppins;
      font-weight: 500px;
      font-size: 15px;
      color: white;
      span {
        color: #dacf0c;
      }
    }
    .search-input {
      color: #9b9b9b;
      background-color: #494949;
      border: 1px solid #9b9b9b;
      height: 25px;
      margin-top: 15px;
      font-family: poppins;
      float: right;
      position: absolute;
      left: 220px;
      top: 10px;
    }
    .search-icon {
      position: absolute;
      top: 32px;
      left: 365px;
      color: #9b9b9b;
    }
  }
}

.filter-row {
  display: flex;
  flex-wrap: wrap;
  .item {
    flex: auto; /* explanation below */
    margin: 5px;
    height: 100px;
  }
}
</style>
