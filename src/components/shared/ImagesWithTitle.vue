<template>
  <div class="wrapper">
    <div class="title">
      <h3>{{ title }}</h3>
      <h4 v-if="subTitle">{{ subTitle }}</h4>
    </div>
    <div class="content">
      <slot name="content"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImagesWithTitle",
  props: {
    title: String,
    subTitle: String
  },
  data() {
    return {};
  }
};
</script>


<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  margin-bottom: 60px;

  .title {
    font-weight: bold;
    margin-bottom: 20px;

    h3 {
      font-size: 1.5rem;
    }

    h4 {
      font-size: 1.1rem;
      color: rgba(0, 0, 0, 0.7);
      margin-top: 10px;
    }
  }

  .content {
    display: flex;
  }
}
</style>
