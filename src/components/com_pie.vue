<template>
  <div class="com_pie">
    <div class="conrtaintitle" v-if="pie_echarts_title_show">
      <div class="title">
        <!-- <div>{{ com_piedata.title }}</div> -->
        <div>{{ com_piedata.title }}</div>
      </div>
    </div>
    <div ref="refchartsdiv" class="classchartsdiv" v-show="!splitpieflag"></div>
    <div class="classchartsdiv" v-show="splitpieflag">
      <div class="splitpie" ref="shucai"></div>
      <div class="splitpie" ref="pifayi"></div>
      <div class="splitpie" ref="pifaer"></div>
    </div>
  </div>
</template>
<script>
import echarts from "echarts";
export default {
  data() {
    return {
      com_piedata: "",
      pie_echarts_title_show: true,
      splitpieflag: false,
    };
  },
  props: ["pieData"],
  watch: {
    pieData: function (newval) {
      console.log(newval);
      this.com_piedata = newval;
    },
  },
  methods: {
    initcharts() {
      // var _this=this;
      var myChart = echarts.init(this.$refs.refchartsdiv);
      // var c=1,d=2;
      this.com_piedata = this.pieData;
      console.log("this.com_piedata", this.com_piedata);
      var option;
      if (this.com_piedata.flag === "vegetableskind") {
        option = {
          color: this.com_piedata.color,
          legend: {
            orient: "vartical",
            x: "left",
            top: "center",
            left: "55%",
            bottom: "0%",
            data: this.com_piedata.xdata,
            itemWidth: 8,
            itemHeight: 8,
            textStyle: {
              color: "#fff",
            },
            formatter: function (name) {
              return "" + name;
            },
          },
          series: [
            {
              type: "pie",
              radius: ["30%", "70%"],
              center: ["30%", "45%"],
              minAngle: 2,
              avoidLabelOverlap: false,
              itemStyle: {
                normal: {
                  borderColor: "#ffffff",
                  borderWidth: 1,
                },
              },
              label: {
                show: false,
                position: "center",
                formatter: "{text|{b}}\n{c} ({d}%)",
                rich: {
                  text: {
                    color: "#fff",
                    fontSize: 14,
                    align: "center",
                    verticalAlign: "middle",
                    padding: 8,
                  },
                  value: {
                    color: "#8693F3",
                    fontSize: 24,
                    align: "center",
                    verticalAlign: "middle",
                  },
                },
              },
              emphasis: {
                label: {
                  show: true,
                  fontSize: "20",
                  fontWeight: "bold",
                },
              },
              labelLine: {
                show: false,
              },
              data: this.com_piedata.ydata,
            },
          ],
        };
        myChart.currentIndex = -1;

        setInterval(function () {
          var dataLen = option.series[0].data.length;
          // 取消之前高亮的图形
          myChart.dispatchAction({
            type: "downplay",
            seriesIndex: 0,
            dataIndex: myChart.currentIndex,
          });
          myChart.currentIndex = (myChart.currentIndex + 1) % dataLen;
          // 高亮当前图形
          myChart.dispatchAction({
            type: "highlight",
            seriesIndex: 0,
            dataIndex: myChart.currentIndex,
          });
        }, 1000);
        console.log("2>1");
        myChart.setOption(option);

        window.addEventListener("resize", function () {
          myChart.resize();
        });
      }
      if (this.com_piedata.flag === "productanalyse") {
        this.pie_echarts_title_show = false;
        console.log("productanalyse success");
        option = {
          /*backgroundColor: '#031845',*/
          tooltip: {
            trigger: "item",
            formatter: "{a} <br/>{b}: {c} ({d}%)",
          },
          graphic: {
            elements: [
              {
                type: "image",
                style: {
                  /*image: giftImageUrl,*/
                  width: 50,
                  height: 50,
                },
                left: "center",
                top: "center",
              },
            ],
          },
          title: {
            text: this.com_piedata.title,
            left: "center",
            top: "10%",
            padding: [24, 0],
            textStyle: {
              color: "#fff",
              fontSize: 18,
              align: "center",
            },
          },
          legend: {
            // top: 0,
            orient: "horizontal",
            icon: "circle",
            bottom: 0,
            x: "center",

            textStyle: {
              color: "#fff",
            },
          },
          series: [
            {
              // top: 0,
              // left: 0,
              name: "产量",
              type: "pie",
              radius: ["25%", "35%"],
              color: this.com_piedata.color,

              labelLine: {
                normal: {
                  show: true,
                  length: 10,
                  length2: 10,
                  lineStyle: {
                    width: 1,
                  },
                },
              },
              label: {
                normal: {
                  formatter: "{c|{c}}\n{hr|}\n{d|{d}%--}",
                  rich: {
                    b: {
                      fontSize: 12,
                      color: "#12EABE",
                      align: "left",
                      padding: 4,
                    },
                    hr: {
                      borderColor: "#12EABE",
                      width: "80%",
                      borderWidth: 2,
                      height: 0,
                    },
                    d: {
                      fontSize: 12,
                      color: "#fff",
                      align: "left",
                      padding: 4,
                    },
                    c: {
                      fontSize: 12,
                      color: "#fff",
                      align: "left",
                      padding: 4,
                    },
                  },
                },
              },
              data: this.com_piedata.data,
            },
          ],
        };
        myChart.currentIndex = -1;
        setInterval(function () {
          var dataLen = option.series[0].data.length;
          // 取消之前高亮的图形
          myChart.dispatchAction({
            type: "downplay",
            seriesIndex: 0,
            dataIndex: myChart.currentIndex,
          });
          myChart.currentIndex = (myChart.currentIndex + 1) % dataLen;
          // 高亮当前图形
          myChart.dispatchAction({
            type: "highlight",
            seriesIndex: 0,
            dataIndex: myChart.currentIndex,
          });
        }, 1000);
        myChart.setOption(option);
        window.addEventListener("resize", function () {
          myChart.resize();
        });
      }

      if (this.com_piedata.flag === "saleprice") {
        this.splitpieflag = true;
        //  console.log(this.splitpieflag);
        if (this.com_piedata.vegetablesprice.title === "白菜") {
          console.log("this-----", this.com_piedata.vegetablesprice);
          myChart = echarts.init(this.$refs.shucai);

          option = {
            title: {
              text: this.com_piedata.vegetablesprice.title,
              bottom: 0,
              left: "center",
              textStyle: {
                color: "#dceaf1",
              },
              // padding: 5 5 5 5,
            },
            color: this.com_piedata.vegetablesprice.color,
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
                    value: this.com_piedata.vegetablesprice.data[0].value,
                    label: {
                      fontSize: 30,
                      show: true,
                      position: "center",
                      formatter: "{d}",
                    },
                  },
                  {
                    value: this.com_piedata.vegetablesprice.data[1].value,
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
        }
        if (this.com_piedata.firwholesale.title === "小白菜") {
          myChart = echarts.init(this.$refs.pifayi);
          option = {
            title: {
              text: this.com_piedata.firwholesale.title,
              //  text:'55',
              bottom: 0,
              left: "center",
              textStyle: {
                color: "#dceaf1",
              },
              // padding: 5 5 5 5,
            },
            color: this.com_piedata.firwholesale.color,
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
                    value: this.com_piedata.firwholesale.data[0].value,
                    // value:22,
                    label: {
                      fontSize: 30,
                      show: true,
                      position: "center",
                      formatter: "{d}",
                    },
                  },
                  {
                    value: this.com_piedata.firwholesale.data[1].value,
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
        }
        if (this.com_piedata.secwholesale.title === "大白菜") {
          myChart = echarts.init(this.$refs.pifaer);
          option = {
            title: {
              text: this.com_piedata.secwholesale.title,
              bottom: 0,
              left: "center",
              textStyle: {
                color: "#dceaf1",
              },
              // padding: 5 5 5 5,
            },
            color: this.com_piedata.secwholesale.color,
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
                    value: this.com_piedata.secwholesale.data[0].value,
                    label: {
                      fontSize: 30,
                      show: true,
                      position: "center",
                      formatter: "{d}",
                    },
                  },
                  {
                    value: this.com_piedata.secwholesale.data[1].value,
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
        }
      }
    },
  },

  mounted() {
    this.initcharts();
  },
};
</script>
<style scoped>
.com_pie {
  margin-top: 0.1rem;
  width: 100%;
  height: 1.5rem;
}
.conrtaintitle {
  width: 100%;
  height: 0.26rem;
}
.title {
  position: relative;
  width: 100%;
  height: 0.26rem;
  background: url(../../public/images/b_bj.png) no-repeat;
  background-size: 100% 100%;
}
.title > div {
  width: 0.8rem;
  top: 0;
  height: 0.26rem;
  line-height: 0.17rem;
  text-align: center;
  color: white;
  font-size: 0.09rem;
}
.classchartsdiv {
  width: 100%;
  height: 1.24rem;
  display: flex;
}

.splitpie {
  flex: 1;
  flex: 1;
  width: 0.7rem;
  height: 1.24rem;
}
</style>>
