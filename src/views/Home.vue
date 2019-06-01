<template>
  <main id="home">
    <Header/>
    <Content/>
  </main>
</template>

<script>
import Header from "@/components/Home/Header";
import Content from "@/components/Home/Content";
export default {
  name: "home",
  components: {
    Header,
    Content
  }
};
</script>
