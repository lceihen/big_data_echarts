<template>
  <div class="com_pageheader">
    <div class="timeinfo">2020-10-20 15:35:03 星期二</div>
    <div class="headerinfo">产业大数据展示</div>
  </div>
</template>

<script>
export default {
  name: "pageheader",
};
</script>


<style scoped>
.com_pageheader {
  position: relative;
  width: 100%;
  height: 0.55rem;
  /* border: 0.0125rem white solid; */
  box-sizing: border-box;
  display: flex;
  flex: 1;
  align-items: center;
}
.timeinfo {
  text-align: center;
  left: 0;
  top: 0;
  position: absolute;
  width: 2rem;
  height: 100%;
  font-size: 0.11rem;
  line-height: 0.5rem;
  color: #ffffff;
}
.headerinfo {
  margin: 0 auto;
  /* left: 50%; */
  width: 3rem;
  height: 100%;
  /* transform: translateX(25%); */
  background: url(../../public/images/h_bj.png) no-repeat top center;
  background-size: 100% 100%;
  font-size: 0.2rem;
  color: #ffffff;
  letter-spacing: 0.001rem;
  text-shadow: 0 0 0.3rem #00d8ff;
  line-height: 0.5rem;
  text-align: center;
}
</style>
