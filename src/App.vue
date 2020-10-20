<template>
  <div class="page">
    <pageheader> </pageheader>
    <div id="page_body"></div>
  </div>
</template>

<script>
import pageheader from "./components/pageheader";
export default {
  name: "App",
  components: { pageheader },
};
</script>

<style scoped>
.page {
  position: relative;
  width: 100%;
  height: 100%;
}
#page_body {
  width: 100%;
}
</style>
