<template>
  <Header />
  <Content />
</template>

<script>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Header,
    Content
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  background-color: #383838;
}
#app {
  
}
</style>
