<template>
  <div class="comleftpage">
    <div class="topdiv">
      <div class="topdiv_title">
        <div>{{ dataleftinfo.topinfo.title }}</div>
      </div>
      <div class="topdiv_info">
        <p class="topdiv_info_top">{{ dataleftinfo.topinfo.context}}</p>
        <div class="topdiv_info_bottom">
          <ul>
            <li>{{ "建筑面积: " + dataleftinfo.topinfo.detail.buildarea }}</li>
            <li>{{ "农户总数: " +dataleftinfo.topinfo.detail.familysum }}</li>
            <li>{{ "人口总数: " + dataleftinfo.topinfo.detail.personsum }}</li>
            <li>{{ "年总产值: " + dataleftinfo.topinfo.detail.yearvalueone }}</li>
            <li>{{ "年总产值: " + dataleftinfo.topinfo.detail.yearvaluetwo }}</li>
            <li>{{ "年总产值: " +dataleftinfo.topinfo.detail.yearvaluethr }}</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="centerdiv">
      <div class="topdiv">
        <div class="topdiv_title">
          <div>{{ dataleftinfo.centerinfo.title }}</div>
        </div>
        <div ref="centerecharts" class="classcenterecharts"></div>
      </div>
    </div>
    <div class="bottomdiv">
      <div class="topdiv_title">
        <div>{{ dataleftinfo.bottominfo.title }}</div>
      </div>
      <div ref="bottomecharts" class="classbottomecharts"></div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";

var leftinfo={
  'topinfo' : {
  'title': "基本信息",
  'context':
    "托各地丰富的无公害、应季的果蔬资源、海鲜资源、山地及海域资源以及农村特色人文资源而搭建，集优质资源整合、优化、流通于一体，涵盖有机蔬果产品、特色平价海鲜、农村生态人文旅游",
  'detail': {
    'buildarea': "1168亩",
    'familysum': "867户",
    'personsum': "13万",
    'yearvalueone': "680万",
    'yearvaluetwo': "4651万",
    'yearvaluethr': "4546万",
  }
  },
'centerinfo':{
  'title':'蔬菜类别',
  'color':[
        "#8d7fec",
        "#5085f2",
        "#e75fc3",
        "#f87be2",
        "#f2719a",
        "#fca4bb",
        "#f59a8f",
        "#fdb301",
        "#57e7ec",
        "#cf9ef1",
      ],
      'xdata': [
        "白菜",
        "西红柿",
        "茄子",
        "辣椒",
        "大蒜",
        "莴笋",
        "洋芋",
        "藕",
        "豌豆",
        "玉米",
      ],
      'ydata':  [
        {
          name: "白菜",
          value: 18,
        },
        {
          name: "西红柿",
          value: 16,
        },
        {
          name: "茄子",
          value: 15,
        },
        {
          name: "辣椒",
          value: 14,
        },
        {
          name: "大蒜",
          value: 10,
        },
        {
          name: "莴笋",
          value: 7.9,
        },
        {
          name: "洋芋",
          value: 6.7,
        },
        {
          name: "藕",
          value: 6,
        },
        {
          name: "豌豆",
          value: 4.5,
        },
        {
          name: "玉米",
          value: 3,
        },
      ],

},
'bottominfo':{
'title':'产量/种植面积',
'xdata': [
              "1月",
              "2月",
              "3月",
              "4月",
              "5月",
              "6月",
              "7月",
              "8月",
              "9月",
              "10月",
              "11月",
              "12月",
            ],
            'yAxis':{
              productname:'产量',
              plantname:'种植面积'
            },
            'productbardata':     {'data': [
              2.0,
              4.9,
              7.0,
              23.2,
              25.6,
              76.7,
              135.6,
              162.2,
              32.6,
              20.0,
              6.4,
              3.3,
            ],
            name:'产量'
            } ,
            plantareabardata: 
            {
              'data':[
              2.6,
              5.9,
              9.0,
              26.4,
              28.7,
              70.7,
              175.6,
              182.2,
              48.7,
              18.8,
              6.0,
              2.3,
            ],
            name:'种植面积'
            },
            toggerincreasinglinedata:{
'data':
[
              2.0,
              2.2,
              3.3,
              4.5,
              6.3,
              10.2,
              20.3,
              23.4,
              23.0,
              16.5,
              12.0,
              6.2,
            ],
            name:'同比增加'

            },
            averagelinedata:{
              'data':    [
              4.0,
              3.2,
              2.3,
              5.5,
              4.3,
              11.2,
              15.3,
              22.4,
              21.0,
              13.5,
              12.0,
              10.2,
            ],
            name:'平均增加'
            }
}
};
export default {
  data() {
    return {
      dataleftinfo:leftinfo,
    };
  },
  methods: {
    initcenterecharts() {
      var myChart = echarts.init(this.$refs.centerecharts);
      var option = {
        color: this.dataleftinfo.centerinfo.color,
        legend: {
          orient: "vartical",
          x: "left",
          top: "center",
          left: "55%",
          bottom: "0%",
          data:  this.dataleftinfo.centerinfo.xdata,
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
            data: this.dataleftinfo.centerinfo.ydata,
          },
        ],
      };
      myChart.setOption(option);
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
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    initbottomecharts() {
      var myChart = echarts.init(this.$refs.bottomecharts);
      var option = {
        /*backgroundColor: '#05163B',*/
        tooltip: {
          trigger: "axis",
        },

        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          top: "10%",
          containLabel: true,
        },
        legend: {
          // data: ["产量", "种植面积", "同比增加", "平均产量"],
          textStyle: {
            color: "#fff",
          },
        },
        xAxis: [
          {
            type: "category",
             data:this.dataleftinfo.bottominfo.xdata,
    
            axisLabel: {
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
        yAxis: [
          {
            type: "value",
            name: this.dataleftinfo.bottominfo.yAxis.productname,
            axisLabel: {
              formatter: "{value} 顿",
              textStyle: {
                color: "#2EC7C9", //y轴文字颜色
              },
            },
            axisLine: {
              lineStyle: {
                color: "#01FCE3",
              },
            },
          },
          {
            type: "value",
            name:this.dataleftinfo.bottominfo.yAxis.plantname,
            axisLabel: {
              formatter: "{value} 亩",
              textStyle: {
                color: "#2EC7C9", //y轴文字颜色
              },
            },
          },
        ],
        series: [
          {
            name: this.dataleftinfo.bottominfo.productbardata.name,
            type: "bar",
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "#00FFE3",
                  },
                  {
                    offset: 1,
                    color: "#4693EC",
                  },
                ]),
              },
            },
            data:this.dataleftinfo.bottominfo.productbardata.data 
       
          },
          {
            name: this.dataleftinfo.bottominfo.plantareabardata.name,
            type: "bar",
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "#C1B2EA",
                  },
                  {
                    offset: 1,
                    color: "#8362C6",
                  },
                ]),
              },
            },
            data:this.dataleftinfo.bottominfo.plantareabardata.data

          },
          {
            name: this.dataleftinfo.bottominfo.toggerincreasinglinedata.name,
            type: "line",
            yAxisIndex: 1,
            data:this.dataleftinfo.bottominfo.toggerincreasinglinedata.data, 

            lineStyle: {
              normal: {
                width: 5,
                color: {
                  type: "linear",

                  colorStops: [
                    {
                      offset: 0,
                      color: "#AAF487", // 0% 处的颜色
                    },
                    {
                      offset: 0.4,
                      color: "#47D8BE", // 100% 处的颜色
                    },
                    {
                      offset: 1,
                      color: "#47D8BE", // 100% 处的颜色
                    },
                  ],
                  globalCoord: false, // 缺省为 false
                },
                shadowColor: "rgba(71,216,190, 0.5)",
                shadowBlur: 10,
                shadowOffsetY: 7,
              },
            },
            itemStyle: {
              normal: {
                color: "#AAF487",
                borderWidth: 10,
                /*shadowColor: 'rgba(72,216,191, 0.3)',
                             shadowBlur: 100,*/
                borderColor: "#AAF487",
              },
            },
            smooth: true,
          },
          {
            name: this.dataleftinfo.bottominfo.averagelinedata.name,
            type: "line",
            yAxisIndex: 1,
            data:this.dataleftinfo.bottominfo.averagelinedata.data,
      
            lineStyle: {
              normal: {
                width: 5,
                color: {
                  type: "linear",

                  colorStops: [
                    {
                      offset: 0,
                      color: "#F8B854", // 0% 处的颜色
                    },
                    {
                      offset: 0.4,
                      color: "#DE801C", // 100% 处的颜色
                    },
                    {
                      offset: 1,
                      color: "#DE801C", // 100% 处的颜色
                    },
                  ],
                  globalCoord: false, // 缺省为 false
                },
                shadowColor: "rgba(71,216,190, 0.5)",
                shadowBlur: 10,
                shadowOffsetY: 7,
              },
            },
            itemStyle: {
              normal: {
                color: "#F7AD3E",
                borderWidth: 10,
                /*shadowColor: 'rgba(72,216,191, 0.3)',
                             shadowBlur: 100,*/
                borderColor: "#F7AD3E",
              },
            },
            smooth: true,
          },
        ],
      };

      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });

    },
  },
  
  mounted() {
    this.initcenterecharts();
    this.initbottomecharts();
  },
};
</script>

<style scoped>
.comleftpage {
  height: 5rem;
}
.topdiv {
  width: 100%;
  height: 1.5rem;
}
.centerdiv {
  margin-top: 0.1rem;
  width: 100%;
  height: 1.5rem;
}
.bottomdiv {
  width: 100%;
  height: 1.9rem;
}
.topdiv_title {
  position: relative;
  width: 100%;
  height: 0.26rem;
  background: url(../../public/images/b_bj.png) no-repeat;
  background-size: 100% 100%;
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
.topdiv_info {
  width: 2.4rem;
  height: 1.24rem;
}
.topdiv_info .topdiv_info_top {
  padding: 0.05rem 0.1rem 0 0.1rem;
  font-size: 0.085rem;
  height: 0.57rem;
  color: #029698;
  width: 2.4rem;
  box-sizing: border-box;
}
.topdiv_info .topdiv_info_bottom {
  height: 0.7rem;
  width: 2.4rem;
}
.topdiv_info ul {
  position: relative;
  display: flex;
  flex: 1;
  width: 2.4rem;
  height: 0.7rem;

  flex-wrap: wrap;
}
.topdiv_info li {
  width: 50%;
  height: 0.177rem;
  text-align: center;
  color: white;
  font-size: 0.09rem;
  list-style: none;
  margin-top: 0.02rem;
}
.classcenterecharts {
  width: 100%;
  height: 1.24rem;
}
.classbottomecharts {
  width: 100%;
  height: 1.5rem;
  box-sizing: border-box;
}
</style>