<template>
  <div class="page">
    <pageheader> </pageheader>
    <div id="page_body">
      <leftpage class="classleftpage"></leftpage>
      <centerpage class="classcenterpage"></centerpage>
      <rightpage class="classrightpage"></rightpage>
    </div>
  </div>
</template>

<script>
import pageheader from "./components/pageheader";
import leftpage from "./components/leftpage";
import centerpage from "./components/centerpage";
import rightpage from "./components/rightpage";
export default {
  name: "App",
  components: { pageheader, leftpage, centerpage, rightpage },
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
  display: flex;
  /* height: 7.5rem; */
}
.classleftpage {
  flex: 1;

  background: skyblue;
}
.classcenterpage {
  flex: 2;
  background: thistle;
}
.classrightpage {
  flex: 1;
  background: tomato;
}
</style>
