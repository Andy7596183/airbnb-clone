<template>
  <section class="home-content">
    <TopicCategories/>
    <Recommendations/>
    <AirbnbPlusLink/>
  </section>
</template>

<script>
import TopicCategories from "@/components/Home/TopicCategories";
import Recommendations from "@/components/Home/Recommendations";
import AirbnbPlusLink from "@/components/Home/AirbnbPlusLink";

export default {
  name: "Content",
  components: {
    TopicCategories,
    Recommendations,
    AirbnbPlusLink
  },
  data() {
    return {};
  }
};
</script>


<style lang="scss" scoped>
.home-content {
  padding: 40px 200px;
}
</style>
