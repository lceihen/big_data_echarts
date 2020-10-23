<template>
  <div class="comrightpage">
    <div class="topdiv">
      <div class="show_div">
        <div class="left_title">{{ lefttitleinfo }}</div>
        <div class="right_title">{{ righttitleinfo }}</div>
      </div>
      <div class="leftdiv"></div>
      <div class="rightdiv"></div>
    </div>
    <div class="centerdiv"></div>
    <div class="bottomdiv"></div>
  </div>
</template>

<script>
// import echarts from "echarts";
var topinfo = {
  zuoshou: [{ 座收租金: "10万" }, { 座收租金: "20万" }, { 座收租金: "50万" }],
  shangpu: [
    { 商铺: "10万" },
    { 商铺: "20万" },
    { 商铺: "30万" },
    { 商铺: "40万" },
    { 商铺: "50万" },
    { 商铺: "60万" },
  ],
  baseplace: [
    { 大棚: "560" },
    { 供应企业: "36" },
    { 经销商: "540" },
    { 供应链: "15" },
    { 蔬菜加工基地: "20" },
    { 售后卸载: "29" },
    { 冷藏基地: "10" },
    { 冷藏车: "120" },
  ],
};

export default {
  data() {
    return {
      lefttitleinfo: "商铺信息",
      righttitleinfo: "基地信息",
      datazuoshou: "",

      datashangpu: "",
      databaseplace: "",
    };
  },
  methods: {
    inittopdiv() {
      this.datazuoshou = topinfo.datazuoshou;
      this.shangpu = topinfo.datashangpu;
      this.baseplace = topinfo.baseplace;
    },
  },
  created() {},
  mounted() {
    this.inittopdiv();
  },
};
</script>

<style>
.comrightpage {
  width: 100%;
  height: 1.45rem;
  border: 1px solid purple;
}
.topdiv {
  width: 100%;
  height: 1.46rem;
  border: 1px solid skyblue;
}
.show_div {
  width: 100%;
  height: 0.2rem;
  color: white;
  font-size: 0.08rem;
  display: flex;
  line-height: 0.2rem;
}
.show_div > div {
  flex: 1;
  width: 50%;
  text-align: center;
  cursor: pointer;
}
</style>