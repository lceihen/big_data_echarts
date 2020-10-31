<template>
  <div class="comrightpage">
    <div class="topdiv">
      <div class="show_div">
        <div
          :class="['left_title', flag ? 'titleclass' : '']"
          @click="this.flag = true"
        >
          {{ datainfo.topinfo.shopinfo }}
        </div>
        <div
          :class="['right_title', flag ? '' : 'titleclass']"
          @click="this.flag = false"
        >
          {{ datainfo.topinfo.baseplaceinfo }}
        </div>
      </div>
      <div class="leftdiv" v-show="flag">
        <div :class="'thrdiv'">
          <div
            :class="'sonthrdiv'"
            v-for="(item, index) in datainfo.topinfo.zuoshou"
            :key="index"
          >
            <p>{{ item.name }}</p>
            <div class="costdiv">{{ item.sum }}</div>
            <div class="divlabel">元</div>
          </div>
        </div>

        <div class="firdiv">
          <div
            :class="'sonfirdiv'"
            v-for="(item, index) in datainfo.topinfo.shangpu"
            :key="index"
          >
            <p>{{ item.name }}</p>
            <p>{{ item.sum }}</p>
          </div>
        </div>
      </div>
      <div class="rightdiv" v-show="!flag">
        <ul>
          <li v-for="(item, index) in datainfo.topinfo.baseplace" :key="index">
            {{ item.name + " : " }}
            <span>{{ item.sum }}</span>
            个
          </li>
        </ul>
      </div>
    </div>
    <div class="centerdiv">
      <div class="topdiv_title">
        <div>{{datainfo.saleranking.title}}</div>
      </div>
      <div class="thrtitle">
        <span>{{datainfo.saleranking.place}}</span>
        <span>{{datainfo.saleranking.compared}}</span>
        <span>{{datainfo.saleranking.salevolume}}</span>
      </div>
      <div ref="fontscrolldiv" id="FontScroll">
        <ul :class="'fontscrollul'">
          <li v-for="(item, index) in datainfo.saleranking.baseplace" :key="index">
            <span>{{ item.name }}</span> <span>{{ item.sum }}</span>
            <span>{{ item.sale }}</span>
          </li>
        </ul>
      </div>
    </div>
    <div class="bottomdiv">
      <!-- <div class="topdiv_title">
        <div>{{datainfo.wholesale.vegetablesprice.title}}</div>
      </div>
      <div class="totalecharts">
        <div ref="total_firstdiv"></div>
        <div ref="total_secdiv"></div>
        <div ref="total_thrdiv"></div>
      </div> -->
      <compie :pie-data="datainfo.wholesale"></compie>
    </div>
  </div>
</template>

<script>
import $ from "jquery";
import "../assets/js/fontscroll";
import echarts from "echarts";
import compie from '../components/com_pie';
var info={
  'topinfo' : {
    'shopinfo':'商铺信息',
    'baseplaceinfo':'基地信息',
  zuoshou: [
    { name: "座收租金", sum: "10万" },
    { name: "座收租金", sum: "10万" },
    { name: "座收租金", sum: "10万" },
  ],
  shangpu: [
    { name: "商铺", sum: "20万" },
    { name: "商铺", sum: "30万" },
    { name: "商铺", sum: "40万" },
    { name: "商铺", sum: "50万" },
    { name: "商铺", sum: "60万" },
    { name: "商铺", sum: "70万" },
  ],
    baseplace: [
    { name: "大棚", sum: "560", sale: "10" },
    { name: "供应企业", sum: "36", sale: "10" },
    { name: "经销商", sum: "540", sale: "10" },
    { name: "供应链", sum: "15", sale: "10" },
    { name: "蔬菜加工基地", sum: "20", sale: "10" },
    { name: "售后卸载", sum: "29", sale: "10" },
    { name: "冷藏基地", sum: "10", sale: "10" },
    { name: "冷藏车", sum: "120", sale: "10" },
  ],
  },



'saleranking':{
  'title':'销售排行',
  'place':'名称',
  'salevolume':'销量',
  'compared':'同比',
  baseplace: [
    { name: "大棚", sum: "560", sale: "10" },
    { name: "供应企业", sum: "36", sale: "10" },
    { name: "经销商", sum: "540", sale: "10" },
    { name: "供应链", sum: "15", sale: "10" },
    { name: "蔬菜加工基地", sum: "20", sale: "10" },
    { name: "售后卸载", sum: "29", sale: "10" },
    { name: "冷藏基地", sum: "10", sale: "10" },
    { name: "冷藏车", sum: "120", sale: "10" },
  ],

},
'wholesale':{
  'flag':'saleprice',
  'title':'蔬菜成交价',
  'vegetablesprice':{  'title':'白菜','color':["#4ac7f5", "#edf1f4"],data:[{'name':'蔬菜成交价','value':20},{'name':'second','value':80}]},
'firwholesale':{'title':'小白菜','color':["#e75fc3", "#57e7ec"],data:[{'name':'批发一','value':22},{'name':'second','value':78}]},
'secwholesale':{'title':'大白菜','color':["#57e7ec", "#de801c"],data:[{'name':'批发二','value':12},{'name':'second','value':88}]}
}
}

export default {
  data() {
    return {
      datainfo:info,
  flag:true
    };
  },
    components:{compie},
  methods: {
    inittotal_thrdiv() {
      var myChart = echarts.init(this.$refs.total_thrdiv);
     
      var option = {
        title: {
          text:this.datainfo.wholesale.secwholesale.title,
            bottom: 0,
          left: 'center',
          textStyle: {
            color: "#dceaf1",
          },
          // padding: 5 5 5 5,
        },
        color: ["#25f3e6", "#ffff43"],
        legend: {
          orient: "vertical",
        },
        series: [
          {
            type: "pie",
            radius: ["50%", "70%"],
            avoidLabelOverlap: true,
            label: {
              show: true,
              position: "inner",
            },
            data: [
              {
                value: this.datainfo.wholesale.secwholesale.data[0].value,
                label: {
                  fontSize: 30,
                  show: true,
                  position: "center",
                  formatter: "{d}",
                },
              },
              {
                value: this.datainfo.wholesale.secwholesale.data[1].value,
                label: {
                  show: false,
                  position: "center",
                  formatter: "{d}",
                },
              },
            ],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    inittotal_secdiv() {
      // var _this=this;
      var myChart = echarts.init(this.$refs.total_secdiv);
      var option = {
        title: {
          text:   this.datainfo.wholesale.firwholesale.title,
        //  text:'55',
            bottom: 0,
          left: 'center',
          textStyle: {
            color: "#dceaf1",
          },
          // padding: 5 5 5 5,
        },
        color: ["#25f3e6", "#edf1f4"],
        legend: {
          orient: "vertical",
        },
        series: [
          {
            type: "pie",
            radius: ["50%", "70%"],
            avoidLabelOverlap: true,
            label: {
              show: true,
              position: "inner",
            },
            data: [
              {
                value: this.datainfo.wholesale.firwholesale.data[0].value,
                // value:22,
                label: {
                  fontSize: 30,
                  show: true,
                  position: "center",
                  formatter: "{d}",
                },
              },
              {
                value: this.datainfo.wholesale.firwholesale.data[1].value,
                label: {
                  show: false,
                  position: "center",
                  formatter: "{d}",
                },
              },
            ],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    inittotal_firstdiv() {
      var myChart = echarts.init(this.$refs.total_firstdiv);
      var option = {
        title: {
          text: this.datainfo.wholesale.vegetablesprice.title,
          bottom: 0,
          left: 'center',
          textStyle: {
            color: "#dceaf1",
          },
          // padding: 5 5 5 5,
        },
        color: ["#4ac7f5", "#edf1f4"],
        legend: {
          orient: "vertical",
        },
        series: [
          {
            type: "pie",
            radius: ["50%", "70%"],
            avoidLabelOverlap: true,
            label: {
              show: true,
              position: "inner",
            },
            data: [
              {
                value: this.datainfo.wholesale.vegetablesprice.data[0].value,
                label: {
                  fontSize: 30,
                  show: true,
                  position: "center",
                  formatter: "{d}",
                },
              },
              {
                value:  this.datainfo.wholesale.vegetablesprice.data[1].value,
                label: {
                  show: false,
                  position: "center",
                  formatter: "{d}",
                },
              },
            ],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    initfontscroll() {
      // this.$refs.fontscrolldiv.fontscroll({ time: 2000, num: 1 });
      $(function () {
        $("#FontScroll").myScroll({ time: 2000, num: 1 });
      });
    },
    inittopdiv() {
      this.datazuoshou = info.topinfo.zuoshou;
      this.datashangpu = info.topinfo.shangpu;
      this.databaseplace = info.topinfo.baseplace;
    },
  },

  mounted() {
    this.inittopdiv();
    this.initfontscroll();
    // this.inittotal_firstdiv();
    // this.inittotal_secdiv();
    // this.inittotal_thrdiv();
  },
};
</script>

<style  scoped >
.topdiv {
  width: 100%;
  height: 1.43rem;
  border: 1px solid #38bce9;
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
.titleclass {
  background-color: rgb(56, 188, 233);
}
.leftdiv {
  width: 100%;
  height: 1.23rem;
  position: relative;
}
.rightdiv {
  width: 100%;

  height: 1.23rem;
  box-sizing: border-box;
  position: relative;

  padding: 1px;
}
.thrdiv {
  display: flex;
  justify-content: space-between;
  height: 0.52rem;
  top: 0.15rem;
  padding: 0.1rem;
  box-sizing: border-box;
}
.sonthrdiv {
  width: 0.49rem;
  height: 0.49rem;
}
.sonthrdiv p {
  color: white;
  width: 100%;
  font-size: 0.08rem;
  text-align: center;
}
.sonthrdiv .divlabel {
  color: white;
    display: inline-block;
    width: 30%;
}
.sonthrdiv .costdiv {
  width:70%;
  height: 0.3rem;
  /* margin-left: 20%; */
  display: inline-block;
text-align: center;
  line-height: 0.25rem;
  font-size: 0.12rem;
  color: rgb(198, 202, 55);
  font-weight: 600;
}
.firdiv {
  margin-top: 0.1rem;

  width: 100%;
  height: 0.81rem;
  box-sizing: border-box;
  display: flex;
}
.sonfirdiv {
  width: 0.34rem;
  height: 0.34rem;
  color: white;
  flex: 1;
  border: 1px solid rgb(85, 188, 212);
  margin-left: 0.02rem;
  margin-right: 0.02rem;
}
.sonfirdiv p:nth-of-type(1) {
  height: 0.16rem;
  font-size: 0.1rem;
  line-height: 0.16rem;
  text-align: center;
}
.sonfirdiv p:nth-of-type(2) {
  text-align: center;
  padding-top: 0.02rem;
}
.rightdiv > ul {
  margin-top: 0.2rem;

  width: 100%;
  height: 1rem;
  color: white;

  /* position: absolute; */
}
li {
  list-style: none;
}
.rightdiv > ul > li {
  width: 50%;
  display: inline-block;
  height: 0.177rem;
  text-align: center;
  font-size: 0.09rem;
}
.rightdiv > ul > li > span {
  /* display: inline-block; */
  color: rgb(0, 255, 255);
  font-size: 0.1rem;
}
.centerdiv {
  width: 100%;
  height: 1.6rem;
}
.topdiv_title {
  position: relative;
  width: 100%;
  height: 0.26rem;
  background: url(../../public/images/b_bj.png) no-repeat;
  background-size: 100% 100%;
}
.thrtitle {
  display: flex;

  text-align: center;
}
.thrtitle > span {
  flex: 1;
  color: #61d2ea;
}

.fontscrollul > li {
  width: 100%;
  height: 0.2rem;
  line-height: 0.2rem;
  display: flex;
  cursor: pointer;
}
.fontscrollul > li > span {
  flex: 1;
  font-size: 0.09rem;
  text-align: center;
  color: white;
  border-top: 1px grey dashed;
}
.fontscrollul > li:hover {
  background-color: rgba(91, 192, 222, 0.5);
}
#FontScroll {
  width: 100%;
  height: 1.255rem;
  overflow: hidden;
}
.topdiv_title > div {
  width: 0.8rem;
  top: 0;
  height: 0.26rem;
  line-height: 0.17rem;
  text-align: center;
  color: white;
  font-size: 0.09rem;
}
.bottomdiv {
  width: 100%;
  height: 1.8rem;
}
.totalecharts {
  width: 100%;
  height: 1.5rem;
  display: flex;
}
.totalecharts > div {
  flex: 1;
  width: 33%;
}
</style>