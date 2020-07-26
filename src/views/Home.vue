
<template>
  <div id="app">
    <div id="main" style="width: 375px;height:300px;background:rgb(8,20,67)"></div>
    <div id="main1" style="width: 375px;height:300px;"></div>
    <div id="main2" style="width: 375px;height:200px;background:rgb(8,20,67)"></div>
    <div id="main2" style="width: 375px;height:200px;background:rgb(8,20,67)"></div>
  </div>
</template>
<script>
import echarts from "echarts/lib/echarts"
import "echarts-liquidfill";
export default {
  name: "app",
  data(){
    return{
      temp:25,
      th:56
    }
  },
  methods: {
    drawChart() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById("main"));
      // 指定图表的配置项和数据
      let value = this.temp;
      let title = "温度";
      let int = value.toFixed(2).split(".")[0];
      let float = value.toFixed(2).split(".")[1];
      let option = {
        backgroundColor: "rgb(8,20,67)",
        title: {
          text: "{a|" + int + "}{b|." + float + "}\n{c|" + title + "}",
          x: "center",
          y: "center",
          textStyle: {
            rich: {
              a: {
                fontSize: 48,
                color: "#29EEF3"
              },
              b: {
                fontSize: 20,
                color: "#29EEF3",
                padding: [0, 0, 14, 0]
              },
              c: {
                fontSize: 20,
                color: "#ffffff",
                padding: [5, 0]
              }
            }
          }
        },
        series: [
          {
            type: "gauge",
            radius: "60%",
            clockwise: false,
            startAngle: "90",
            endAngle: "-269.9999",
            splitNumber: 25,
            detail: {
              offsetCenter: [0, -20],
              formatter: " "
            },
            pointer: {
              show: false
            },
            axisLine: {
              show: true,
              lineStyle: {
                color: [
                  [0, "#2CFAFC"],
                  [75 / 100, "#1DE2A4"],
                  [1, "rgba(32,187,252,0.15)"]
                ],
                width: 30
              }
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: true,
              length: 32,
              lineStyle: {
                color: "#051F54",
                width: 6
              }
            },
            axisLabel: {
              show: false
            }
          },
          {
            type: "pie",
            name: "内层细圆环",
            radius: ["43%", "45%"],
            hoverAnimation: false,
            clockWise: false,
            itemStyle: {
              normal: {
                color: "#0C355E"
              }
            },
            label: {
              show: false
            },
            data: [100]
          },
          {
            type: "pie",
            name: "内层环",
            radius: [0, "43%"],
            hoverAnimation: false,
            clockWise: false,
            itemStyle: {
              normal: {
                color: "#02163F"
              }
            },
            label: {
              show: false
            },
            data: [100]
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    },
    drawChart_1() {
      let myChart = this.$echarts.init(document.getElementById("main1"));
      var dataArr =this.th;
      var colorSet = {
        color: "#468EFD"
      };

      var option = {
        backgroundColor: "rgb(8,20,67)",
        title: {
          show: true,
          text: "风速",
          x: "49%",
          y: "55%",
          z: 8,
          textAlign: "center",
          textStyle: {
            color: " #fff ",
            fontSize: 26
          }
        },
        series: [
          {
            name: "内部进度条",
            type: "gauge",
            // center: ['20%', '50%'],
            radius: "60%",

            splitNumber: 10,
            axisLine: {
              lineStyle: {
                color: [
                  [dataArr / 100, colorSet.color],
                  [1, "#111F42"]
                ],
                width: 14
              }
            },
            axisLabel: {
              show: false
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false
            },

            pointer: {
              show: false
            }
          },
          {
            name: "外部刻度",
            type: "gauge",
            //  center: ['20%', '50%'],
            radius: "70%",
            min: 0, //最小刻度
            max: 100, //最大刻度
            splitNumber: 10, //刻度数量
            startAngle: 225,
            endAngle: -45,
            axisLine: {
              show: true,
              lineStyle: {
                width: 2,
                color: [[1, "rgba(0,0,0,0)"]]
              }
            },
            //仪表盘轴线
            axisLabel: {
              show: true,
              color: "#4d5bd1",
              distance: 25,
              formatter: function(v) {
                switch (v + "") {
                  case "0":
                    return "0";
                  case "10":
                    return "10";
                  case "20":
                    return "20";
                  case "30":
                    return "30";
                  case "40":
                    return "40";
                  case "50":
                    return "50";
                  case "60":
                    return "60";
                  case "70":
                    return "70";
                  case "90":
                    return "90";
                  case "100":
                    return "100";
                }
              }
            }, //刻度标签。
            axisTick: {
              show: true,
              splitNumber: 7,
              lineStyle: {
                color: colorSet.color, //用颜色渐变函数不起作用
                width: 2
              },
              length: -8
            }, //刻度样式
            splitLine: {
              show: true,
              length: -20,
              lineStyle: {
                color: colorSet.color //用颜色渐变函数不起作用
              }
            }, //分隔线样式
            detail: {
              show: false
            },
            pointer: {
              show: false
            }
          },
          /*内部*/
          {
            type: "pie",
            radius: ["0", "35%"],
            center: ["50%", "50%"],
            z: 8,
            hoverAnimation: false,
            data: [
              {
                name: "污染程度",
                value: this.th,
                itemStyle: {
                  normal: {
                    color: new echarts.graphic.LinearGradient(0, 1, 0, 0, [
                      {
                        offset: 0,
                        color: "#4FADFD"
                      },
                      {
                        offset: 1,
                        color: "#28E8FA"
                      }
                    ])
                  }
                },
                label: {
                  normal: {
                    rich: {
                      a: {
                        color: "#468EFD",
                        align: "center",
                        fontSize: 50,
                        fontWeight: "bold"
                      }
                    },
                    formatter: function(params) {
                      return "{a|" + params.value + "}";
                    },
                    position: "center",
                    show: true
                  }
                },
                labelLine: {
                  show: false
                }
              }
            ]
          },
          /*外一层*/
          {
            type: "pie",
            radius: "40%",
            startAngle: 220,
            endAngle: -40,
            hoverAnimation: false,
            center: ["50%", "50%"],
            avoidLabelOverlap: false,
            label: {
              show: false
            },
            labelLine: {
              show: false
            },
            data: [
              {
                value: 1
              }
            ],
            itemStyle: {
              normal: {
                color: {
                  type: "linear",
                  x: 0,
                  y: 0,
                  x2: 0,
                  y2: 1,
                  colorStops: [
                    {
                      offset: 0,
                      color: "rgba(69, 161, 255,0.8)"
                    },
                    {
                      offset: 1,
                      color: "rgba(69, 161, 255,0.5)"
                    }
                  ]
                }
              }
            }
          },
          //外二层圈
          {
            type: "pie",
            radius: "45%",
            center: ["50%", "50%"],
            avoidLabelOverlap: false,
            z: 0,
            hoverAnimation: false,
            label: {
              show: false
            },
            labelLine: {
              show: false
            },
            data: [
              {
                value: 1
              }
            ],
            itemStyle: {
              normal: {
                color: {
                  type: "linear",
                  x: 0,
                  y: 0,
                  x2: 0,
                  y2: 1,
                  colorStops: [
                    {
                      offset: 0,
                      color: "rgba(69, 161, 255,0.5)"
                    },
                    {
                      offset: 1,
                      color: "rgba(69, 161, 255,0.3)"
                    }
                  ]
                }
              }
            }
          },
          //最外层圈
          {
            type: "pie",
            radius: "50%",
            center: ["50%", "50%"],
            avoidLabelOverlap: false,
            z: 0,
            hoverAnimation: false,
            label: {
              show: false
            },
            labelLine: {
              show: false
            },
            data: [
              {
                value: 1
              }
            ],
            itemStyle: {
              normal: {
                color: {
                  type: "linear",
                  x: 0,
                  y: 0,
                  x2: 0,
                  y2: 1,
                  colorStops: [
                    {
                      offset: 0,
                      color: "rgba(69, 161, 255,0.3)"
                    },
                    {
                      offset: 1,
                      color: "rgba(69, 161, 255,0)"
                    }
                  ]
                }
              }
            }
          }
        ]
      };
      myChart.setOption(option);
    },
  sum (m,n){
    var num = Math.floor(Math.random()*(m - n) + n);
    return num
}
  },
  mounted() {
    this.drawChart();
    this.drawChart_1();
  },
  created(){
    setInterval(()=>{
      this.temp=this.sum(18,35)
      this.th=this.sum(18,35)
      this.drawChart();
      this.drawChart_1();
    },3000)
  }
};
</script>
<style scoped>
</style>
