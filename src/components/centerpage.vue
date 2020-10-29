<template>
  <div class="com_centerdiv">
    <div class="top_div">
      <div class="top_div_title">
        <ul class="first_ul">
          <li>{{ datacenterinfo.map.plantbaseplace.title }}</li>
          <li>{{ datacenterinfo.map.connected.title }}</li>
        </ul>
        <ul class="second_ul">
          <li
            class="fontdiv"
            v-for="(item, index) in datacenterinfo.map.plantbaseplace.amount"
            :key="index"
          >
            {{ item }}
          </li>

          <li class="font_sim">个</li>
          <li
            class="fontdiv"
            v-for="(item, index) in datacenterinfo.map.connected.amount"
            :key="index"
          >
            {{ item }}
          </li>

          <li class="font_sim">%</li>
        </ul>
      </div>
      
      <div class="map" ref="map_china" ></div>
    </div>
    <div class="bottom_div">
      <div class="left_div" ref="left_div_echarts"></div>
      <div class="right_div" ref="right_div_echarts"></div>
    </div>
    <div class="mask"  v-show="datacenterinfo.map.pointshow" @click="closecommappointpage()">
     
    </div> 
    <mappointpage ref="commappointpage" :father-flag="datacenterinfo.map.pointshow"  @closecommappointpage="closecommappointpage">
      <p>{{mappointslot.name}}</p>
<p>{{mappointslot.selfvalue}}</p>
    </mappointpage>

  </div>
</template>

<script>
import echarts from "echarts";
import mappointpage from './mappointpage';
import "echarts/map/js/china.js";
var centerinfo = {
  map: {
    plantbaseplace: {
      title: "种植基地",
      amount: "365",
    },
    connected: {
      title: "已接入",
      amount: "83",
    },
    pointshow:false,
    mapdetail: {
      geoCoordMap: {
        海门: [121.15, 31.89],
        鄂尔多斯: [109.781327, 39.608266],
        招远: [120.38, 37.35],
        舟山: [122.207216, 29.985295],
        齐齐哈尔: [123.97, 47.33],
        盐城: [120.13, 33.38],
        赤峰: [118.87, 42.28],
        青岛: [120.33, 36.07],
        乳山: [121.52, 36.89],
        金昌: [102.188043, 38.520089],
        泉州: [118.58, 24.93],
        莱西: [120.53, 36.86],
        日照: [119.46, 35.42],
        胶南: [119.97, 35.88],
        南通: [121.05, 32.08],
        拉萨: [91.11, 29.97],
        云浮: [112.02, 22.93],
        梅州: [116.1, 24.55],
        文登: [122.05, 37.2],
        上海: [121.48, 31.22],
        攀枝花: [101.718637, 26.582347],
        威海: [122.1, 37.5],
        承德: [117.93, 40.97],
        厦门: [118.1, 24.46],
        汕尾: [115.375279, 22.786211],
        潮州: [116.63, 23.68],
        丹东: [124.37, 40.13],
        太仓: [121.1, 31.45],
        曲靖: [103.79, 25.51],
        烟台: [121.39, 37.52],
        福州: [119.3, 26.08],
        瓦房店: [121.979603, 39.627114],
        即墨: [120.45, 36.38],
        抚顺: [123.97, 41.97],
        玉溪: [102.52, 24.35],
        张家口: [114.87, 40.82],
        阳泉: [113.57, 37.85],
        莱州: [119.942327, 37.177017],
        湖州: [120.1, 30.86],
        汕头: [116.69, 23.39],
        昆山: [120.95, 31.39],
        宁波: [121.56, 29.86],
        湛江: [110.359377, 21.270708],
        揭阳: [116.35, 23.55],
        荣成: [122.41, 37.16],
        连云港: [119.16, 34.59],
        葫芦岛: [120.836932, 40.711052],
        常熟: [120.74, 31.64],
        东莞: [113.75, 23.04],
        河源: [114.68, 23.73],
        淮安: [119.15, 33.5],
        泰州: [119.9, 32.49],
        南宁: [108.33, 22.84],
        营口: [122.18, 40.65],
        惠州: [114.4, 23.09],
        江阴: [120.26, 31.91],
        蓬莱: [120.75, 37.8],
        韶关: [113.62, 24.84],
        嘉峪关: [98.289152, 39.77313],
        广州: [113.23, 23.16],
        延安: [109.47, 36.6],
        太原: [112.53, 37.87],
        清远: [113.01, 23.7],
        中山: [113.38, 22.52],
        昆明: [102.73, 25.04],
        寿光: [118.73, 36.86],
        盘锦: [122.070714, 41.119997],
        长治: [113.08, 36.18],
        深圳: [114.07, 22.62],
        珠海: [113.52, 22.3],
        宿迁: [118.3, 33.96],
        咸阳: [108.72, 34.36],
        铜川: [109.11, 35.09],
        平度: [119.97, 36.77],
        佛山: [113.11, 23.05],
        海口: [110.35, 20.02],
        江门: [113.06, 22.61],
        章丘: [117.53, 36.72],
        肇庆: [112.44, 23.05],
        大连: [121.62, 38.92],
        临汾: [111.5, 36.08],
        吴江: [120.63, 31.16],
        石嘴山: [106.39, 39.04],
        沈阳: [123.38, 41.8],
        苏州: [120.62, 31.32],
        茂名: [110.88, 21.68],
        嘉兴: [120.76, 30.77],
        长春: [125.35, 43.88],
        胶州: [120.03336, 36.264622],
        银川: [106.27, 38.47],
        张家港: [120.555821, 31.875428],
        三门峡: [111.19, 34.76],
        锦州: [121.15, 41.13],
        南昌: [115.89, 28.68],
        柳州: [109.4, 24.33],
        三亚: [109.511909, 18.252847],
        自贡: [104.778442, 29.33903],
        吉林: [126.57, 43.87],
        阳江: [111.95, 21.85],
        泸州: [105.39, 28.91],
        西宁: [101.74, 36.56],
        宜宾: [104.56, 29.77],
        呼和浩特: [111.65, 40.82],
        成都: [104.06, 30.67],
        大同: [113.3, 40.12],
        镇江: [119.44, 32.2],
        桂林: [110.28, 25.29],
        张家界: [110.479191, 29.117096],
        宜兴: [119.82, 31.36],
        北海: [109.12, 21.49],
        西安: [108.95, 34.27],
        金坛: [119.56, 31.74],
        东营: [118.49, 37.46],
        牡丹江: [129.58, 44.6],
        遵义: [106.9, 27.7],
        绍兴: [120.58, 30.01],
        扬州: [119.42, 32.39],
        常州: [119.95, 31.79],
        潍坊: [119.1, 36.62],
        重庆: [106.54, 29.59],
        台州: [121.420757, 28.656386],
        南京: [118.78, 32.04],
        滨州: [118.03, 37.36],
        贵阳: [106.71, 26.57],
        无锡: [120.29, 31.59],
        本溪: [123.73, 41.3],
        克拉玛依: [84.77, 45.59],
        渭南: [109.5, 34.52],
        马鞍山: [118.48, 31.56],
        宝鸡: [107.15, 34.38],
        焦作: [113.21, 35.24],
        句容: [119.16, 31.95],
        北京: [116.46, 39.92],
        徐州: [117.2, 34.26],
        衡水: [115.72, 37.72],
        包头: [110, 40.58],
        绵阳: [104.73, 31.48],
        乌鲁木齐: [87.68, 43.77],
        枣庄: [117.57, 34.86],
        杭州: [120.19, 30.26],
        淄博: [118.05, 36.78],
        鞍山: [122.85, 41.12],
        溧阳: [119.48, 31.43],
        库尔勒: [86.06, 41.68],
        安阳: [114.35, 36.1],
        开封: [114.35, 34.79],
        济南: [117, 36.65],
        德阳: [104.37, 31.13],
        温州: [120.65, 28.01],
        九江: [115.97, 29.71],
        邯郸: [114.47, 36.6],
        临安: [119.72, 30.23],
        兰州: [103.73, 36.03],
        沧州: [116.83, 38.33],
        临沂: [118.35, 35.05],
        南充: [106.110698, 30.837793],
        天津: [117.2, 39.13],
        富阳: [119.95, 30.07],
        泰安: [117.13, 36.18],
        诸暨: [120.23, 29.71],
        郑州: [113.65, 34.76],
        哈尔滨: [126.63, 45.75],
        聊城: [115.97, 36.45],
        芜湖: [118.38, 31.33],
        唐山: [118.02, 39.63],
        平顶山: [113.29, 33.75],
        邢台: [114.48, 37.05],
        德州: [116.29, 37.45],
        济宁: [116.59, 35.38],
        荆州: [112.239741, 30.335165],
        宜昌: [111.3, 30.7],
        义乌: [120.06, 29.32],
        丽水: [119.92, 28.45],
        洛阳: [112.44, 34.7],
        秦皇岛: [119.57, 39.95],
        株洲: [113.16, 27.83],
        石家庄: [114.48, 38.03],
        莱芜: [117.67, 36.19],
        常德: [111.69, 29.05],
        保定: [115.48, 38.85],
        湘潭: [112.91, 27.87],
        金华: [119.64, 29.12],
        岳阳: [113.09, 29.37],
        长沙: [113, 28.21],
        衢州: [118.88, 28.97],
        廊坊: [116.7, 39.53],
        菏泽: [115.480656, 35.23375],
        合肥: [117.27, 31.86],
        武汉: [114.31, 30.52],
        大庆: [125.03, 46.58],
      },
      fromto: [
        [{ name: "广州" }, { name: "宁波" }],
        [{ name: "广州" }, { name: "北京" }],
        [{ name: "广州" }, { name: "呼和浩特" }],
        [{ name: "宁波" }, { name: "北京" }],
      ],
      pointname: [
        {'name':'广州','value':'30'},
        {'name':'宁波','value':'20'},
        {'name':'北京','value':'78'},
        {'name':'呼和浩特','value':'2'}
        ],
     temvalue:[{'name':'广州'}]
    },
  },
  saleprecentdata: {
    title: "销量",
    data: [110, 20, 36, 10, 50, 80, 100, 60],
    color: ["#0035f9", "#f36f8a", "#ffff43", "#25f3e6"],
    yAxis: {
      data: ["白菜", "西红柿", "茄子", "辣椒", "大蒜", "莴笋", "洋芋", "藕"],
    },
  },
  productanalyse: {
    title: "产量分析",
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
};
export default {
  
  data() {
    return {
      mappointslot:"",
      datacenterinfo: centerinfo,
    };
  },
  components:{mappointpage},
  methods: {

closecommappointpage(){
  

this.datacenterinfo.map.pointshow=false;
},
    echart_map() {
      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(this.$refs.map_china);
      var _this = this;
      var convertData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
          var dataItem = data[i];
          var fromCoord =
            _this.datacenterinfo.map.mapdetail.geoCoordMap[dataItem[0].name];
          var toCoord =
            _this.datacenterinfo.map.mapdetail.geoCoordMap[dataItem[1].name];
          if (fromCoord && toCoord) {
            res.push([
              {
                coord: fromCoord,
              },
              {
                coord: toCoord,
              },
            ]);
          }
        }
        return res;
      };
      //点的形成
      var pointData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
          var dataItem = data[i].name;
var Selfvalue=data[i].value;
          var point = _this.datacenterinfo.map.mapdetail.geoCoordMap[dataItem];
          res.push({ name: dataItem, value: point ,selfvalue:Selfvalue});
        }
        return res;
      };

      var option = {
               tooltip: {
                trigger: 'item',
                backgroundColor: 'rgba(166, 200, 76, 0.82)',
                borderColor: '#FFFFCC',
                showDelay: 0,
                hideDelay: 0,
                enterable: true,
                transitionDuration: 0,
                extraCssText: 'z-index:20',
                formatter: function(params) {
          
                    // console.log("p",params)
                if(params.componentSubType=="effectScatter")
                   {
                     var res = "";
                    var name = params.data.name;
                    var value = params.data.selfvalue;
                    res = "<span style='color:#fff;'>" + name + "</span><br/>数据：" + value;
                    return res;
                   }
           
                }
            },
        geo: {
          map: "china",
          itemStyle: {
            // areaColor: '#323c48',
            // borderColor: '#111',
            color: "rgba(51, 69, 89, .5)", //地图背景色
            borderColor: "#516a89", //省市边界线00fcff 516a89
            borderWidth: 1,
          },
          roam: true,
          emphasis: {
            itemStyle: {
              color: "rgba(37, 43, 61, .5)", //悬浮背景
            },
            label: {
              show: false,
            },
          },
        },
        series: [
          {
            color: "#01e1f5",
            type: "lines",
            symbol: ["none", "arrow"],
            zlevel: 10,
            effect: {
              symbol: ["triangle"],
              show: true,
              period: 4,
              trailLength: 0.02,
              //  color: 'red',
              symbolSize: 7,
            },
            lineStyle: {
              normal: {
                //   color: '#a6c84c',

                width: 1,
                opacity: 1, //尾迹线条透明度
                curveness: 0.4,
              },
            },
            data: convertData(this.datacenterinfo.map.mapdetail.fromto),
          },
          {
            type: "effectScatter",
            coordinateSystem: "geo",
            zlevel: 20,
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
                formatter: "{b}",
                fontSize: 13,
              },
              emphasis: {
                show: true,
              },
            },
            symbol: "circle",
            symbolSize: 15, //圆环大小,
            itemStyle: {
              normal: {
                show: false,
                color: "#01e1f5",
              },
            },
            data: pointData(this.datacenterinfo.map.mapdetail.pointname),

            //  [  {'name':'广州',
            //     'value':[113.23,23.16]  }]
          },
        ],
      };
myChart.on('click', 'series.effectScatter',function (params) {
    console.log(params);
_this.datacenterinfo.map.pointshow=true;
console.log(_this.datacenterinfo.map.pointshow);
_this.mappointslot=params.data;
});

      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });

    },

    initleftcharts() {
      var _this = this;
      var myChart = echarts.init(this.$refs.left_div_echarts);
      // var data = [110, 20, 36, 10, 50, 80, 100, 60];
      var sum = 0;
      var newpercentdata = [];
      for (
        var i = 0;
        i < _this.datacenterinfo.saleprecentdata.data.length;
        i++
      ) {
        sum += _this.datacenterinfo.saleprecentdata.data[i];
      }
      for (
        var j = 0;
        j < _this.datacenterinfo.saleprecentdata.data.length;
        j++
      ) {
        newpercentdata.push(
          ((_this.datacenterinfo.saleprecentdata.data[j] / sum) * 100).toFixed(
            2
          )
        );
      }
      var option = {
        color: this.datacenterinfo.saleprecentdata.color,
        // color:["#0035f9", "#f36f8a", "#ffff43", "#25f3e6"],
        grid: {
          left: "8%",
          right: "10%",
          top: "12%",
          bottom: "18%",
          containLabel: true,
        },
        yAxis: {
          data: this.datacenterinfo.saleprecentdata.yAxis.data,
          // data: [
          //   "白菜",
          //   "西红柿",
          //   "茄子",
          //   "辣椒",
          //   "大蒜",
          //   "莴笋",
          //   "洋芋",
          //   "藕",
          // ],
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
            // name:this.datacenterinfo.saleprecentdata.title,
            name: "52",
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
            data: newpercentdata,
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
          text: this.datacenterinfo.productanalyse.title,
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
            color: this.datacenterinfo.productanalyse.color,
            // [
            //   "#00FFFF",
            //   "#44EAB1",
            //   "#7BDD43",
            //   "#FEBE12",
            //   "#EBEC2F",
            //   "#FF7C44",
            //   "#FA3E5F",
            //   "#6635EF",
            //   "#FFAFDA",
            // ],
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
            data: this.datacenterinfo.productanalyse.data,
            // data: [
            //   {
            //     value: 100,
            //     name: "一号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "二号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "三号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "四号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "五号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "六号大棚",
            //   },
            //   {
            //     value: 100,
            //     name: "七号大棚",
            //   },
            // ],
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

  mounted() {
    this.echart_map();
    this.initleftcharts();
    this.initrightcharts();
    // this.initfunction();
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

  z-index: 10;
}
.bottom_div {
  width: 4.85rem;
  height: 1.7rem;
  display: flex;
  border: 1px solid #55bcd4;
}
.left_div {
  flex: 1;
  height: 100%;
}
.right_div {
  flex: 1;
  height: 100%;
}
.mask {
	width:100%;
	height:100%;
	background:gray;
position: fixed;
	top:0;
	left:0;
	z-index:100;
	opacity:0.6;
	/* display:none; */
	
}
.mappointpage{
    z-index:10100;
}
</style>