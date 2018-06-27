<template>
  <div class="wrapper">
    <div class="header">
      <text class="header__text">Posts</text>
    </div>
    <list class="list">
      <Card v-for="list in lists" :key="list" :list="list"/>
    </list>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
var stream = weex.requireModule("stream");
var modal = weex.requireModule("modal");
export default {
  name: "App",
  components: {
    Card
  },
  created() {
    stream.fetch(
      {
        url: "https://godinner-backend.herokuapp.com/app/feed",
        method: "GET",
        type: "json"
      },
      response => {
        if (!response.ok) {
          this.lists = ["Falha"];
        } else {
          this.lists = response.data.reverse();
        }
      }
    );
  },
  data() {
    return {
      lists: []
    }; 
  }
};
</script>

<style lang="scss" scoped>
.header {
  width: 750px;
  border-bottom-color: rgba(0, 0, 0, 0.1);
  border-bottom-width: 2px;
  background-color: white;
  padding-bottom: 30px;
  margin-bottom: 20px;
  &__text {
    font-size: 80px;
    font-weight: bold;
    margin-top: 60px;
    margin-left: 50px;
  }
}
.wrapper {
  justify-content: center;
  align-items: center;
  background-color: #fafafa;
}
</style>