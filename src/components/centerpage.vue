<template>
  <div class="com_centerdiv">
    <div class="top_div">
      <div class="top_div_title">
        <ul class="first_ul">
          <li>{{ first_ul_title }}</li>
          <li>{{ second_ul_title }}</li>
        </ul>
        <ul class="second_ul">
          <li class="fontdiv">3</li>
          <li class="fontdiv">6</li>
          <li class="fontdiv">5</li>
          <li class="font_sim">个</li>
          <li class="fontdiv">8</li>
          <li class="fontdiv">3</li>
          <li class="font_sim">%</li>
        </ul>
      </div>
      <div class="map" ref="map_china"></div>
    </div>
    <div class="bottom_div">
      <div class="left_div" ref="left_div_echarts"></div>
      <div class="right_div" ref="right_div_echarts"></div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
import "echarts/map/js/china.js";
export default {
  data() {
    return {
      first_ul_title: "种植基地",
      //  first_ul_sum:"",
      second_ul_title: "已接入",
    };
  },
  methods: {
    echart_map() {
      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(this.$refs.map_china);

      var chinaGeoCoordMap = {
        黑龙江: [127.9688, 45.368],
        内蒙古: [110.3467, 41.4899],
        吉林: [125.8154, 44.2584],
        北京市: [116.4551, 40.2539],
        辽宁: [123.1238, 42.1216],
        河北: [114.4995, 38.1006],
        天津: [117.4219, 39.4189],
        山西: [112.3352, 37.9413],
        陕西: [109.1162, 34.2004],
        甘肃: [103.5901, 36.3043],
        宁夏: [106.3586, 38.1775],
        青海: [101.4038, 36.8207],
        新疆: [87.9236, 43.5883],
        西藏: [91.11, 29.97],
        四川: [103.9526, 30.7617],
        重庆: [108.384366, 30.439702],
        山东: [117.1582, 36.8701],
        河南: [113.4668, 34.6234],
        江苏: [118.8062, 31.9208],
        安徽: [117.29, 32.0581],
        湖北: [114.3896, 30.6628],
        浙江: [119.5313, 29.8773],
        福建: [119.4543, 25.9222],
        江西: [116.0046, 28.6633],
        湖南: [113.0823, 28.2568],
        贵州: [106.6992, 26.7682],
        云南: [102.9199, 25.4663],
        广东: [113.12244, 23.009505],
        广西: [108.479, 23.1152],
        海南: [110.3893, 19.8516],
        上海: [121.4648, 31.2891],
      };
      var chinaDatas = [
        [
          {
            name: "黑龙江",
            value: 0,
          },
        ],
        [
          {
            name: "内蒙古",
            value: 0,
          },
        ],
        [
          {
            name: "吉林",
            value: 0,
          },
        ],
        [
          {
            name: "辽宁",
            value: 0,
          },
        ],
        [
          {
            name: "河北",
            value: 0,
          },
        ],
        [
          {
            name: "天津",
            value: 0,
          },
        ],
        [
          {
            name: "山西",
            value: 0,
          },
        ],
        [
          {
            name: "陕西",
            value: 0,
          },
        ],
        [
          {
            name: "甘肃",
            value: 0,
          },
        ],
        [
          {
            name: "宁夏",
            value: 0,
          },
        ],
        [
          {
            name: "青海",
            value: 0,
          },
        ],
        [
          {
            name: "新疆",
            value: 0,
          },
        ],
        [
          {
            name: "西藏",
            value: 0,
          },
        ],
        [
          {
            name: "四川",
            value: 0,
          },
        ],
        [
          {
            name: "重庆",
            value: 0,
          },
        ],
        [
          {
            name: "山东",
            value: 0,
          },
        ],
        [
          {
            name: "河南",
            value: 0,
          },
        ],
        [
          {
            name: "江苏",
            value: 0,
          },
        ],
        [
          {
            name: "安徽",
            value: 0,
          },
        ],
        [
          {
            name: "湖北",
            value: 0,
          },
        ],
        [
          {
            name: "浙江",
            value: 0,
          },
        ],
        [
          {
            name: "福建",
            value: 0,
          },
        ],
        [
          {
            name: "江西",
            value: 0,
          },
        ],
        [
          {
            name: "湖南",
            value: 0,
          },
        ],
        [
          {
            name: "贵州",
            value: 0,
          },
        ],
        [
          {
            name: "广西",
            value: 0,
          },
        ],
        [
          {
            name: "海南",
            value: 0,
          },
        ],
        [
          {
            name: "上海",
            value: 1,
          },
        ],
      ];

      var convertData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
          var dataItem = data[i];
          var fromCoord = chinaGeoCoordMap[dataItem[0].name];
          var toCoord = [116.4551, 40.2539];
          if (fromCoord && toCoord) {
            res.push([
              {
                coord: fromCoord,
                value: dataItem[0].value,
              },
              {
                coord: toCoord,
              },
            ]);
          }
        }
        return res;
      };
      var series = [];
      [["北京市", chinaDatas]].forEach(function (item) {
        console.log(item);
        series.push(
          {
            type: "lines",
            zlevel: 2,
            effect: {
              show: true,
              period: 4, //箭头指向速度，值越小速度越快
              trailLength: 0.02, //特效尾迹长度[0,1]值越大，尾迹越长重
              symbol: "arrow", //箭头图标
              symbolSize: 5, //图标大小
            },
            lineStyle: {
              normal: {
                width: 1, //尾迹线条宽度
                opacity: 1, //尾迹线条透明度
                curveness: 0.3, //尾迹线条曲直度
              },
            },
            data: convertData(item[1]),
          },
          {
            type: "effectScatter",
            coordinateSystem: "geo",
            zlevel: 2,
            rippleEffect: {
              //涟漪特效
              period: 4, //动画时间，值越小速度越快
              brushType: "stroke", //波纹绘制方式 stroke, fill
              scale: 4, //波纹圆环最大限制，值越大波纹越大
            },
            label: {
              normal: {
                show: true,
                position: "right", //显示位置
                offset: [5, 0], //偏移设置
                formatter: function (params) {
                  //圆环显示文字
                  return params.data.name;
                },
                fontSize: 13,
              },
              emphasis: {
                show: true,
              },
            },
            symbol: "circle",
            symbolSize: function (val) {
              return 5 + val[2] * 5; //圆环大小
            },
            itemStyle: {
              normal: {
                show: false,
                color: "#f00",
              },
            },
            data: item[1].map(function (dataItem) {
              return {
                name: dataItem[0].name,
                value: chinaGeoCoordMap[dataItem[0].name].concat([
                  dataItem[0].value,
                ]),
              };
            }),
          },
          //被攻击点
          {
            type: "scatter",
            coordinateSystem: "geo",
            zlevel: 2,
            rippleEffect: {
              period: 4,
              brushType: "stroke",
              scale: 4,
            },
            label: {
              normal: {
                show: true,
                position: "right",
                //offset:[5, 0],
                color: "#0f0",
                formatter: "{b}",
                textStyle: {
                  color: "#0f0",
                },
              },
              emphasis: {
                show: true,
                color: "#f60",
              },
            },
            symbol: "pin",
            symbolSize: 50,
            data: [
              {
                name: item[0],
                value: chinaGeoCoordMap[item[0]].concat([10]),
              },
            ],
          }
        );
      });

      var option = {
        tooltip: {
          trigger: "item",
          backgroundColor: "rgba(166, 200, 76, 0.82)",
          borderColor: "#FFFFCC",
          showDelay: 0,
          hideDelay: 0,
          enterable: true,
          transitionDuration: 0,
          extraCssText: "z-index:100",
          formatter: function (params) {
            //根据业务自己拓展要显示的内容
            var res = "";
            var name = params.name;
            var value = params.value[params.seriesIndex + 1];
            res =
              "<span style='color:#fff;'>" +
              name +
              "</span><br/>数据：" +
              value;
            return res;
          },
        },
        /*backgroundColor:"#013954",*/
        visualMap: {
          //图例值控制
          min: 0,
          max: 1,
          calculable: true,
          show: false,
          color: ["#f44336", "#fc9700", "#ffde00", "#ffde00", "#00eaff"],
          textStyle: {
            color: "#fff",
          },
        },
        geo: {
          map: "china",
          zoom: 1.2,
          label: {
            emphasis: {
              show: false,
            },
          },
          roam: true, //是否允许缩放
          itemStyle: {
            normal: {
              color: "rgba(51, 69, 89, .5)", //地图背景色
              borderColor: "#516a89", //省市边界线00fcff 516a89
              borderWidth: 1,
            },
            emphasis: {
              color: "rgba(37, 43, 61, .5)", //悬浮背景
            },
          },
        },
        series: series,
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },

    initleftcharts() {
      var myChart = echarts.init(this.$refs.left_div_echarts);
      var data = [110, 20, 36, 10, 50, 80, 100, 60];
      var sum = 0;
      var percentdata = [];
      for (var i = 0; i < data.length; i++) {
        sum += data[i];
      }
      for (var j = 0; j < data.length; j++) {
        percentdata.push(((data[j] / sum) * 100).toFixed(2));
      }
      var option = {
        color: ["#0035f9", "#f36f8a", "#ffff43", "#25f3e6"],
        grid: {
          left: "8%",
          right: "10%",
          top: "12%",
          bottom: "18%",
          containLabel: true,
        },
        yAxis: {
          data: [
            "白菜",
            "西红柿",
            "茄子",
            "辣椒",
            "大蒜",
            "莴笋",
            "洋芋",
            "藕",
          ],
          axisTick: {
            show: false,
          },
          axisLabel: {
            formatter: "{value} ",
            textStyle: {
              color: "#2EC7C9", //X轴文字颜色
            },
          },
          axisLine: {
            lineStyle: {
              color: "#01FCE3",
            },
          },
        },

        xAxis: [
          {
            axisTick: {
              show: false,
            },
            type: "value",
            // max: 100,
            splitNumber: 5,
            axisLabel: {
              formatter: "{value}%",
              show: true,
              textStyle: {
                color: "#ebf8ac", //X轴文字颜色
              },
            },
            axisLine: {
              lineStyle: {
                color: "#01FCE3",
              },
            },
          },
        ],
        series: [
          {
            name: "销量",
            type: "bar",
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "#25f3e6",
                  },
                  {
                    offset: 1,
                    color: "#4693EC",
                  },
                ]),
              },
            },
            barWidth: "55%",
            label: {
              normal: {
                show: true,
                position: "right",
                formatter: "{c}%",
                textStyle: {
                  color: "#ffffff",
                },
              },
            },
            data: percentdata,
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    initrightcharts() {
      var myChart = echarts.init(this.$refs.right_div_echarts);
      var option = {
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
          text: "产量分析",
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
          data: [
            "一号大棚",
            "二号大棚",
            "三号大棚",
            "四号大棚",
            "五号大棚",
            "六号大棚",
            "七号大棚",
          ],
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
            color: [
              "#00FFFF",
              "#44EAB1",
              "#7BDD43",
              "#FEBE12",
              "#EBEC2F",
              "#FF7C44",
              "#FA3E5F",
              "#6635EF",
              "#FFAFDA",
            ],
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
            data: [
              {
                value: 100,
                name: "一号大棚",
              },
              {
                value: 100,
                name: "二号大棚",
              },
              {
                value: 100,
                name: "三号大棚",
              },
              {
                value: 100,
                name: "四号大棚",
              },
              {
                value: 100,
                name: "五号大棚",
              },
              {
                value: 100,
                name: "六号大棚",
              },
              {
                value: 100,
                name: "七号大棚",
              },
            ],
          },
        ],
      };

      myChart.setOption(option);
      myChart.currentindex = -1;

      setInterval(() => {
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

      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
  },
  created() {},
  mounted() {
    this.echart_map();
    this.initleftcharts();
    this.initrightcharts();
  },
};
</script>

<style scoped>
.top_div {
  background: url(../../public/images/d_bj.png) no-repeat;
  background-size: 100% 100%;
  width: 4.85rem;
  height: 3.2rem;
  position: relative;
  box-sizing: border-box;
  padding-top: 0.1px;
}
li {
  list-style: none;
}
.top_div_title {
  position: absolute;
  top: 0.3rem;
  left: 0.3rem;
}
.first_ul > li {
  display: inline-block;
  height: 0.2rem;
  width: 0.8rem;
  font-size: 0.08rem;
  color: white;
}
.second_ul li {
  margin-left: 0.05rem;
  text-align: center;
}
.font_sim {
  display: inline-block;
  width: 0.16rem;
  font-size: 0.08rem;
  height: 0.21rem;
  color: white;
}
.fontdiv {
  color: white;
  display: inline-block;
  width: 0.16rem;
  font-size: 0.15rem;
  height: 0.21rem;
  background: #55bcd4;
}
.map {
  width: 3rem;
  height: 2.6rem;
  position: relative;
  margin: 0.4rem 0.02rem 0.02rem 1.5rem;

  z-index: 9999;
}
.bottom_div {
  width: 4.85rem;
  height: 1.7rem;
  display: flex;
}
.left_div {
  flex: 1;
  height: 100%;
}
.right_div {
  flex: 1;
  height: 100%;
}
</style>