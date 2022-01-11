<template>
  <div class="content-container">
    <img src="../assets/big-picture.png" alt="Baner" />
    <img src="../assets/big-picture.png" alt="Baner" />
    <Search @search-game="search" :contentLength="contentData.length" />
    <div class="spinner" v-if="!contentData.length">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    <div class="row" v-if="contentData.length">
      <div
        v-for="(game, index) in contentData.slice(0, contentLength)"
        :key="index"
        class="item"
      >
        <img :src="getImageUrl(game.templateImg)" alt="game-banner" />
        <span>{{ game.templateName }}</span>
      </div>
    </div>
  </div>
  <button v-if="contentData.length" class="show-more-btn" @click="loadMore">
    Show More
  </button>
</template>
<script>
import Search from "../components/Search.vue";

export default {
  name: "Content",
  components: {
    Search,
  },
  data() {
    return {
      contentData: [],
      contentLength: 60,
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    search(searchQuery) {
      if (searchQuery) {
        let filteredContentData = this.contentData.filter((item) =>
          item.templateName.includes(searchQuery)
        );
        this.contentData = filteredContentData;
      }
    },
    loadMore() {
      if (this.contentLength > this.contentData.length) return;
      this.contentLength = this.contentLength + 60;
    },
    async fetchData() {
      const response = await fetch(
        "https://betwill.com/api/game/getgametemplates/1/1/1"
      );
      const data = await response.json();
      data.GameTemplates.forEach((gameTemplate) => {
        const gameTemplateName = data.GameTemplateNameTranslations.find(
          (templateName) => templateName.GameTemplateId === gameTemplate.ID
        );
        const gameTemplateImg = data.GameTemplateImages.find(
          (templateImage) => templateImage.GameTemplateId === gameTemplate.ID
        );
        if (gameTemplateName && gameTemplateImg) {
          this.contentData.push({
            templateName: gameTemplateName.Value,
            templateImg: gameTemplateImg.CdnUrl,
            defaultOrdering: gameTemplate.DefaultOrdering,
          });
        }
      });
      this.sort();
      console.log(this.contentData);
    },
    getImageUrl(img) {
      if (img) {
        return `https://static.inpcdn.com/${img}`;
      }
    },
    sort() {
      this.contentData.sort((a, b) => {
        return a.defaultOrdering - b.defaultOrdering;
      });
    },
  },
};
</script>

<style scoped lang="scss">
.content-container {
  padding: 0 305px;
  margin-top: 40px;
}
.content-container img:first-of-type {
  margin-right: 44px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  .item {
    flex: auto;
    height: 200px;
    width: 300px;
    margin: 40px 10px 74px 10px;
    text-align: center;
    span {
      font-size: 16px;
      color: white;
      font-family: Poppins;
    }
    img {
      margin-bottom: 10px;
    }
  }
}
.spinner {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
  margin-left: 610px;
  div {
    box-sizing: border-box;
    display: block;
    position: absolute;
    width: 64px;
    height: 64px;
    margin: 8px;
    border: 8px solid #fff;
    border-radius: 50%;
    animation: spinner 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: #fff transparent transparent transparent;
  }
  div:nth-child(1) {
    animation-delay: -0.45s;
  }
  div:nth-child(2) {
    animation-delay: -0.3s;
  }
  div:nth-child(3) {
    animation-delay: -0.15s;
  }
}
@keyframes spinner {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.show-more-btn {
  width: 155px;
  height: 32px;
  background-color: #fff209;
  outline: none;
  cursor: pointer;
  border-radius: 4px;
  border: none;
  font-family: Poppins;
  float: right;
  margin: 46px 318px 118px 106px;
}
</style>
