<template>
  <ImagesWithTitle title="探索Airbnb">
    <template #content>
      <a v-for="(topic, index) in topics" :key="index" href="#" class="topic">
        <div class="topic-img" :style="{'background-image': `url(${topic.img})`}"/>
        <div class="topic-name">{{ topic.title }}</div>
      </a>
    </template>
  </ImagesWithTitle>
</template>

<script>
import ImagesWithTitle from "@/components/shared/ImagesWithTitle";
import unsplash from "@/assets/helpers/api/unsplash";

export default {
  name: "TopicCategories",
  components: {
    ImagesWithTitle
  },
  data() {
    return {
      topics: [
        {
          title: "房源和精品旅店",
          img:
            "https://a0.muscache.com/4ea/air/v2/pictures/8b7519ec-2c82-4c09-8233-fd4d2715bbf9.jpg?t=r:w100-h70-sfit,e:fjpg-c80"
        },
        {
          title: "體驗",
          img:
            "https://a0.muscache.com/4ea/air/v2/pictures/a77ee672-e790-4362-8cc5-52bec1371ece.jpg?t=r:w100-h70-sfit,e:fjpg-c80"
        },
        {
          title: "餐廳",
          img:
            "https://a0.muscache.com/4ea/air/v2/pictures/da2d8e97-90b7-409f-94ac-5ab0327c289b.jpg?t=r:w100-h70-sfit,e:fjpg-c80"
        }
      ]
    };
  }
};
</script>


<style lang="scss" scoped>
.topic {
  width: 300px;
  display: flex;
  margin-right: 20px;
  box-shadow: 1px 1px 1px 0px lightgray;

  .topic-img {
    flex: 1;
    height: 70px;
  }

  .topic-name {
    flex: 2;
    display: flex;
    justify-content: center;
    align-items: center;
    border: #e9e9e9 solid 1px;
  }
}
</style>

