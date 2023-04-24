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
            <button @click="reorderGrid">Organizar</button>
            <button @click="reorderGrid">Organizar</button>
            <button @click="reorderGrid">Organizar</button>
        </div>
    </div>
    <div class="grid-stack" ref="grid">
    <div
        v-for="widget in content.data"
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
import { ref, onMounted, onBeforeMount, reactive} from 'vue'
import { GridStack } from 'gridstack'
import 'gridstack/dist/gridstack.min.css'
import 'gridstack/dist/gridstack-extra.min.css'
import charts from './moch/charts'
const content = reactive({data:[]})

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

    makeWidgets(content.data)
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

onMounted(() => {
    initGridStack()
})

onBeforeMount(()=>{
    content.data = charts
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
