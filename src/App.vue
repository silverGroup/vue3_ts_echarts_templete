<script setup lang="ts">
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts';
import 'echarts-liquidfill';
const liquidHieght = ref(0)
const chartpanel = ref(null)
const liquidFill=ref(null)
function initChart() {
  const data = [10,20]
  const myChart = echarts.init(chartpanel.value)
  const liquidFillChart = echarts.init(liquidFill.value)
  const status = (data[0] + data[1] < 100) && (data[0] + data[1] > 2)
  if ((data[0] + data[1]) >= 100) {
    if (data[0] >= 100) {
      data[1] = 0
      data[0] = 100
    } else {
      data[1] = 100 - data[0]
    }
  }
  const options = {
    xAxis: {
      data: ['百分比'],
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      axisLabel: {
        show: false
      }
    },
    yAxis: {
      splitLine: {
        show: false
      },
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      axisLabel: {
        show: false
      }
    },
    grid: {
      top: '0',
      bottom: '11.7px'
    },
    series: [
      {
        name: '最底部立体圆邊框',
        type: 'pictorialBar',
        symbolSize: [70, 22],
        symbolOffset: [0, 12],
        z: 6,
        itemStyle: {
          opacity: 1,
          normal: {
            color: data[0] ? '#41b166' : data[1] ? '#f6af5d' : '#E9ECEE'
          }
        },
        silent: true,
        data: [100]
      },
      {
        name: '最底部立体圆',
        type: 'pictorialBar',
        symbolSize: [68, 21],
        symbolOffset: [0, 11],
        z: 6,
        itemStyle: {
          normal: {
            color: data[0] ? '#41b166' : data[1] ? '#f88151' : data[0] & data[1] ? 'transparent' : '#E9ECEE'
          }
        },
        silent: true,
        cursor: 'none',
        data: [100]
      },
      {
        name: '中间立体圆',
        type: 'pictorialBar',
        symbolSize: [70, 21],
        symbolOffset: [0, -11],
        z: 6,
        itemStyle: {
          normal: {
            color: data[0] && data[1] ? '#91DEA9' : 'transparent'
          }
        },
        silent: true,
        cursor: 'none',
        data: [
          {
            value: data[0],
            symbolPosition: 'end'
          }
        ]
      },
      {
        name: '中间立体圆',
        type: 'pictorialBar',
        symbolSize: [70, 22],
        symbolOffset: [0, -12],
        z: 8,
        silent: true,
        cursor: 'none',
        itemStyle: {
          normal: {
            color: data[0] && data[1] ? '#f88151' : data[0] & !data[1] ? '#91DEA9' : 'transparent'
          }
        },
        data: [
          {
            value: data[0],
            symbolPosition: 'end'
          }
        ]
      },
      {
        // 绿色底部立体柱
        stack: '1',
        type: 'bar',
        itemStyle: {
          normal: {
            borderType: 'solid',
            opacity: 1,
            color: {
              type: 'linear',
              x: 0,
              y: 0,
              x2: 0,
              y2: 1,
              colorStops: [
                {
                  offset: 0,
                  color: '#91DEA9'
                },
                {
                  offset: 0.5,
                  color: '#6ED28C'

                },
                {
                  offset: 1,
                  color: '#49BA6B'
                }
              ],
              globalCoord: false // 缺省为 false
            }
          }
        },
        z: 7,
        silent: true,
        barWidth: 70,
        barGap: '-100%',
        data: [data[0]]
      },
      {
        // 黄色中间段立柱
        stack: '1',
        type: 'bar',
        z: 8,
        itemStyle: {
          normal: {
            opacity: 1,
            borderWidth: 0,
            color: {
              type: 'linear',
              x: 0,
              y: 0,
              x2: 0,
              y2: 1,
              colorStops: [
                {
                  offset: 0,
                  color: data[1] > 2 ? '#F5D061' : 'transparent'
                },

                {
                  offset: 1,
                  color: data[1] > 2 ? '#F78C54' : 'transparent'
                }
              ],
              globalCoord: false // 缺省为 false
            }
          }
        },
        silent: true,
        barWidth: 70,
        barGap: '-100%',
        data: [data[1]]
      },
      {
        // 上部立体柱
        stack: '1',
        type: 'bar',
        z: 1,
        itemStyle: {
          normal: {
            barBorderWidth: 0,
            opacity: 0.39,
            color: {
              type: 'linear',
              x: 0,
              y: 0,
              x2: 0,
              y2: 1,
              colorStops: [
                {
                  offset: 0.87,
                  color: 'rgba(219,222,224,0.4)'
                },
                {
                  offset: 0.61,
                  color: ' rgba(219,223,227,0.6)'
                },
                {
                  offset: 0.29,
                  color: '#E2E6EE'
                },
                {
                  offset: 0.15,
                  color: '#E2E2EB'
                },
                {
                  offset: 0,
                  color: '#FFFFFF'
                }
              ],
              globalCoord: false // 缺省为 false
            }
          }
        },
        silent: true,
        barWidth: 70,
        barGap: '-100%',
        data: [100 - data[0] - data[1]]
      }
    ]
  }
  const optionsli = {
    xAxis: {
      data: ['百分比'],
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      axisLabel: {
        show: false
      }
    },
    grid: {
      top: '0',
      bottom: '11.7px'
    },
    yAxis: {
      splitLine: {
        show: false
      },
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      axisLabel: {
        show: false
      }
    },
    series: [
      {
        type: 'liquidFill',
        radius: '69px',
        // center: ['50%', +((data[0] + data[1] > 30) ? (95 - data[0] - data[1] + 2) : (95 - data[0] - data[1] + 1)) + '%'],
        z: 4,
        data: [0.2,
          {
            value: 0.3,
            direction: 'left',
            symbolPosition: 'end'
          }],
        shape: 'container',
        cursor: 'none',
        silent: true,
        color: [
          {
            type: 'linear',
            x: 0, // 右
            y: 0, // 上
            x2: 1, // 左
            y2: 1, // 下
            colorStops: [
              {
                offset: 1,
                color: status && data[1] ? (data[1] < 2 ? '#ef9565' : '#F5D061') : status && data[0] ? '#91DEA9' : 'transparent'
              },
              {
                offset: 0,
                color: status && data[1] ? (data[1] < 2 ? '#ef9565' : '#F5D061') : status && data[0] ? '#91DEA9' : 'transparent'
              }
            ],
            globalCoord: false
          }
        ],
        outline: { // 轮廓设置
          show: false,
          itemStyle: {
            borderWidth: 0
          }
        },
        itemStyle: { shadowBlur: 0, opacity: 0.9 },
        amplitude: 2,
        backgroundStyle: {
          shadowColor: 'transparent',
          opacity: 0,
          color: 'rgba(233,236,238,0.3)'
        },
        label: {
          show: false
        }
      }
    ]
  }
  if (options) {
    myChart.setOption(options)
  }
  liquidHieght.value = data[0] + data[1] > 100 || data[0] + data[1] < 2 ? '-999' : (data[0] + data[1] - 0.3)
  if (optionsli) {
    liquidFillChart.setOption(optionsli)
  }
}
onMounted(() => {
  console.log(`the component is now mounted.`)
  initChart()
  //       window.addEventListener('resize', () => {
  //   myChart.resize()
  // })
})
</script>

<template>
    <div class="echarts-box">
      <div v-if="videoTipStatus" class="transtion-echart" />
      <div id="chart-panel" ref="chartpanel" />
      <div id="chart-liquidFill" ref="liquidFill" :style="{bottom:liquidHieght+'%'}" />
    </div>
</template>

<style scoped>
.echarts-box{
  width: 100px;
  height: calc(100vh - 420px);
  margin-top: 16px;
  position: relative;
}
#chart-panel ,#test{
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 10
}
#chart-liquidFill{
  position: absolute;
  bottom: 0;
  left:50%;
  height: 40px;
  width: 69px;
  transform: translate(-50%,0);
}
</style>
