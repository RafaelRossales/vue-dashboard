// eslint-disable-next-line @typescript-eslint/no-unused-vars
<template>
  <div class="p-8 bg-gray-50 min-h-screen">
    <div class="teste"></div>
    <div class="header">
        <div class="img-section">
            <img src="./assets/marcopolo-logo.png" class="logo">
        </div>
        <div>Analitics</div>
        <div class="btn-section">
            <!-- <div> -->
                <button @click="reorderGrid">Organizar</button>
                <button @click="reorderGrid">Organizar</button>
                <button @click="reorderGrid">Organizar</button>
            <!-- </div> -->
        </div>
    </div>
    <div class="grid-stack" ref="grid">
    <div
        v-for="widget in widgets"
        :key="widget.id"
        :id="widget.id"
        :gs-id="widget.id"
        :gs-x="widget.grid.x"
        :gs-y="widget.grid.y"
        :gs-w="widget.grid.w"
        :gs-h="widget.grid.h"
      >
        <div
          class="grid-stack-item-content p-4 bg-white rounded-md shadow-md flex items-center justify-center text-gray-700"
        >
          <div class="widget-header" style="cursor: move;">
            <span class="text-2xl">{{ widget.title }}</span>
          </div>
          <div class="widget-body">
            <apexchart
              :options="widget.content.chartOptions"
              :series="widget.content.series"
              height="200"
              ref="chart"
            ></apexchart>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { GridStack } from 'gridstack'
import 'gridstack/dist/gridstack.min.css'
import 'gridstack/dist/gridstack-extra.min.css'
import { shuffle } from 'lodash'
// import ApexCharts from 'apexcharts'

const widgets = ref([
  {
    id: 1,
    title: 'First Widget',
    content: {
    chartOptions: {
        chart: {
            id: 'basic-bar',
        },
    xaxis: {
        categories: [
            'Jan',
            'Feb',
            'Mar',
            'Apr',
            'May',
            'Jun',
            'Jul',
            'Aug',
            'Sep',
            'Oct',
            'Nov',
            'Dec',
        ],
    },
    },
    series: [
        {
        name: 'Series 1',
        data: [30, 40, 45, 50, 49, 60, 70, 91, 125, 135, 152, 170],
        },
    ],
    },
    grid: {
      x: 0,
      y: 0,
      w: 2,
      h: 3,
    },
  },
    {
    id: 2,
    title: 'First abg',
    content: {
      chartOptions: {
        chart: {
            height: 350,
            type: 'area'
            },
            dataLabels: {
              enabled: false
            },
            stroke: {
              curve: 'smooth'
            },
            xaxis: {
              type: 'datetime',
              categories: ["2018-09-19T00:00:00.000Z", "2018-09-19T01:30:00.000Z", "2018-09-19T02:30:00.000Z", "2018-09-19T03:30:00.000Z", "2018-09-19T04:30:00.000Z", "2018-09-19T05:30:00.000Z", "2018-09-19T06:30:00.000Z"]
            },
            tooltip: {
              x: {
                format: 'dd/MM/yy HH:mm'
              },
            },
          },
      series: [{
            name: 'series1',
            data: [31, 40, 28, 51, 42, 109, 100]
          }, {
            name: 'series2',
            data: [11, 32, 45, 32, 34, 52, 41]
          }],
    },
    grid: {
      x: 6,
      y: 5,
      w: 2,
      h: 3,
    },
    },
    {
        id:3,
        title:'First Widget',
        content:{
            chartOptions:{
                chart: {
              type: 'bar',
              height: 350
            },
            plotOptions: {
              bar: {
                horizontal: false,
                columnWidth: '55%',
                endingShape: 'rounded'
              },
            },
            dataLabels: {
              enabled: false
            },
            stroke: {
              show: true,
              width: 2,
              colors: ['transparent']
            },
            xaxis: {
              categories: ['Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct'],
            },
            yaxis: {
              title: {
                text: '$ (thousands)'
              }
            },
            fill: {
              opacity: 1
            },
            tooltip: {
              y: {
                formatter: function (val) {
                  return "$ " + val + " thousands"
                }
              }
            }
        },
        series: [{
            name: 'Net Profit',
            data: [44, 55, 57, 56, 61, 58, 63, 60, 66]
            }, {
                name: 'Revenue',
                data: [76, 85, 101, 98, 87, 105, 91, 114, 94]
            }, {
                name: 'Free Cash Flow',
                data: [35, 41, 36, 26, 45, 48, 52, 53, 41]
            }],
        },
        grid: {
            x: 10,
            y: 5,
            w: 2,
            h: 3,
        },
    },
    {
        id:4,
        title:'acd',
        content:{
            series: [{
            data: [400, 430, 448, 470, 540, 580, 690, 1100, 1200, 1380]
            }],
            chartOptions: {
            chart: {
                type: 'bar',
                height: 350
            },
            plotOptions: {
                bar: {
                    borderRadius: 4,
                    horizontal: true,
                }
            },
            dataLabels: {
              enabled: false
            },
            xaxis: {
              categories: ['South Korea', 'Canada', 'United Kingdom', 'Netherlands', 'Italy', 'France', 'Japan',
                'United States', 'China', 'Germany'
              ],
            }
        },
    },
        grid: {
            x: 0,
            y: 0,
            w: 1,
            h: 3,
        },
    },
    {
        id:5,
        title:'acd',
        content:{
            series: [{
            data: [400, 430, 448, 470, 540, 580, 690, 1100, 1200, 1380]
            }],
            chartOptions: {
            chart: {
                type: 'bar',
                height: 350
            },
            plotOptions: {
                bar: {
                    borderRadius: 4,
                    horizontal: true,
                }
            },
            dataLabels: {
              enabled: false
            },
            xaxis: {
              categories: ['South Korea', 'Canada', 'United Kingdom', 'Netherlands', 'Italy', 'France', 'Japan',
                'United States', 'China', 'Germany'
              ],
            }
        },
    },
        grid: {
            x: 1,
            y: 1,
            w: 1,
            h: 3,
        },
    },
    {
        id:6,
        title:'Teste',
        content:{
         chartOptions: {
            chart: {
              type: 'area',
              height: 350,
              stacked: true,
              events: {
                selection: function (chart, e) {
                  console.log(new Date(e.xaxis.min))
                }
              },
            },
            colors: ['#008FFB', '#00E396', '#CED4DC'],
            dataLabels: {
              enabled: false
            },
            stroke: {
              curve: 'smooth'
            },
            fill: {
              type: 'gradient',
              gradient: {
                opacityFrom: 0.6,
                opacityTo: 0.8,
              }
            },
            legend: {
              position: 'top',
              horizontalAlign: 'left'
            },
            xaxis: {
              type: 'datetime'
            },
          },
        series: [
            {
              name: 'South',
              data: generateDayWiseTimeSeries(new Date('11 Feb 2017 GMT').getTime(), 20, {
                min: 10,
                max: 60
              })
            },
            {
              name: 'North',
              data: generateDayWiseTimeSeries(new Date('11 Feb 2017 GMT').getTime(), 20, {
                min: 10,
                max: 20
              })
            },
            {
              name: 'Central',
              data: generateDayWiseTimeSeries(new Date('11 Feb 2017 GMT').getTime(), 20, {
                min: 10,
                max: 15
              })
            }
          ],
        },
        grid: {
        x: 6,
        y: 5,
        w: 3,
        h: 3,
        },
    }
])

let grid = null

function initGridStack() {
grid = GridStack.init({
    column: 4,
    cellHeight: 100,
    row:0,
    minRow: 1,
    margin: 10,
    handle: '.widget-header',
  })



  grid.on('resizestop', (event, element) => {
    const chartRef = element.querySelector('.apexcharts')
    if (chartRef) {
      const chart = chartRef.__vue__.chart
      chart.resize()
    }
  })

  makeWidgets(widgets.value)
}

function makeWidgets(widgets) {
  widgets.forEach((widget) => {
    makeWidget(widget)
  })
}

function reorderGrid() {
  grid.compact();
}


function makeWidget(item) {
  const elSelector = `#${item.id}`
  return grid.makeWidget(elSelector)
}

function generateDayWiseTimeSeries(baseval, count, yrange) {
  var i = 0;
  var series = [];
  while (i < count) {
    var x = baseval;
    var y =
      Math.floor(Math.random() * (yrange.max - yrange.min + 1)) + yrange.min;

    series.push([x, y]);
    baseval += 86400000;
    i++;
  }
  return series;
}

onMounted(() => {
  initGridStack()
})
</script>
<style scoped>

.widget-header{
    background-color: rgb(255, 255, 255);
    padding: 5px;
    text-align: center;
    font-size: 20px;
}
.widget-header:hover{
    background-color: rgb(228, 228, 228);
}

.grid-stack-item-content {
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    background-color: rgb(255, 255, 255);
    border-radius:10px;
}

</style>


// <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="reorderGrids">Reorder Grids</button>