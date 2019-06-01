<template>
  <ImagesWithTitle title="為您推薦">
    <template #content>
      <a v-for="(rec, index) in recommendations" :key="index" href="#">
        <div
          class="rec-img"
          :style="{'background-color': 'gray', 'background-image': `url(${rec.img})`}"
        />
        <div class="rec-text">
          <h4 class="rec-city">{{ rec.city }}</h4>
          <span class="rec-avg-price">每晚平均${{ rec.average }}TWD</span>
        </div>
      </a>
    </template>
  </ImagesWithTitle>
</template>

<script>
import ImagesWithTitle from "@/components/shared/ImagesWithTitle";
import unsplash from "@/assets/helpers/api/unsplash";

export default {
  name: "Recommendations",
  components: {
    ImagesWithTitle
  },
  data() {
    return {
      recommendations: [
        {
          city: "巴黎",
          average: 3536,
          // prettier-ignore
          img: "https://a0.muscache.com/im/pictures/998b4270-25d7-4850-8ccf-4350b9a5ab05.jpg?aki_policy=large",
          isLoaded: false
        },
        {
          city: "東京",
          average: 2740,
          // prettier-ignore
          img: "https://a0.muscache.com/im/pictures/60145c65-7c36-4ac5-8129-6ae9a0d27a81.jpg?aki_policy=large",
          isLoaded: false
        },
        {
          city: "倫敦",
          average: 3953,
          // prettier-ignore
          img: "https://a0.muscache.com/im/pictures/6729455e-af21-4dc3-bfdf-332393d407a8.jpg?aki_policy=large",
          isLoaded: false
        },
        {
          city: "洛杉磯",
          average: 4263,
          // prettier-ignore
          img: "https://a0.muscache.com/im/pictures/82af5bc4-ed5b-44d9-9209-ac0f2fbf8986.jpg?aki_policy=large",
          isLoaded: false
        },
        {
          city: "巴塞隆納",
          average: 3429,
          // prettier-ignore
          img: "https://a0.muscache.com/im/pictures/6db93b37-3d4b-49c0-af00-c184a9dd6305.jpg?aki_policy=large",
          isLoaded: false
        }
      ]
    };
  },
  created() {}
};
</script>


<style lang="scss" scoped>
a {
  flex: 1;
  position: relative;
  border-radius: 4px;
  height: 360px;

  .rec-img {
    height: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    margin: 0 15px;
    border-radius: 4px;

    &:first-child {
      margin-left: 0;
    }

    &:last-child {
      margin-right: 0;
    }
  }

  .rec-text {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    bottom: 30px;
    color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    font-weight: bolder;

    h4 {
      font-size: 1.2rem;
      margin-bottom: 10px;
    }
  }
}
</style>
