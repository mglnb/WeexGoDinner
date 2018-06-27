<template>

    <cell class="card"> 
      <div class="card__header">
        <image class="card__header__image" :src="list.restaurant.avatar_url"/>
        <div class="card__header__wrapper">
          <text class="card__header__name">{{list.restaurant.name}}</text>
          <text class="card__header__info">{{list.created_at}}</text>
        </div>
      </div> 
      <div class="card__content">
        <text class="card__content__title">{{list.title}}</text>
        <text class="card__content__desc">{{content}}...</text>
        <text @click="changeContent" class="card__content__desc card__content__desc--more">{{fullData ?"Ver menos" :"Ver mais"}}</text>
        <image class="card__content__image" :src="list.image_url"/>
      </div>
      <div class="card__footer">
      </div>
    </cell>

</template>

<script>
// https://png.icons8.com/metro/1600/like.png
// https://upload.wikimedia.org/wikipedia/commons/thumb/c/c8/Love_Heart_symbol.svg/1000px-Love_Heart_symbol.svg.png
export default {
  computed: {
    content() {
      return this.fullData
        ? this.list.content
            .replace(/<\/?[^>]+(>|$)/g, "") 
            .replace(/\s|&nbsp;/, "")
        : this.list.content
            .replace(/<\/?[^>]+(>|$)/g, "")
            .replace(/\s|&nbsp;/, "")
            .substring(0, 50);
    }
  },
  methods: {
    changeContent() {
      this.fullData = !this.fullData;
    }
  },
  data() {
    return {
      fullData: false
    };
  },
  props: {
    list: {
      type: Object
    }
  }
};
</script>

<style scoped lang="scss">
.card {
  &__header {
    flex-direction: row;
    margin-bottom: 30px;
    &__image {
      width: 70px;
      height: 70px;
      border-radius: 50%;
      margin-right: 20px;
    }
    &__info {
      font-size: 20px;
      color: #bbb;
      margin-top: 10px;
    }
  }
  &__content {
    background-color: #ffffff;
    width: 650px;

    // margin-top: 35px;
    flex-direction: column;
    height: 600px;
    padding: 30px;
    align-items: flex-start;
    &__title {
      font-size: 26px;
      text-align: left;
      font-weight: bold;
      margin-bottom: -15px;
    }
    &__desc {
      font-size: 22px;
      color: #bbbbbb;
      margin-bottom: 10px;
      &--more {
        color: #9999ff;
      }
    }
    &__image {
      width: 580px;
      height: 400px;
      border-radius: 20px;
    }
  }
  &__footer {
    background-color: white;
    width: 650px;
    margin-bottom: 120px;
    padding-left: 30px;
    padding-top: 20px;
    padding-bottom: 30px;
    &__like {
      width: 90px;
      height: 90px;
      justify-content: center;
      align-items: center;
      border-width: 2px;
      border-color: red;
      border-radius: 50%;
      padding: 20px;
      opacity: 0.1;
      &__text {
        font-size: 40px;
        color: white;
      }
    }
  }
}
</style>



