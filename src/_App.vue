<template>
  <div class="p-8 bg-gray-50 min-h-screen">
    <div class="grid-stack">
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
            <p>Widget content goes here</p>
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

const widgets = ref([
  {
    id: 1,
    title: 'First Widget',
    grid: {
      x: 0,
      y: 0,
      w: 2,
      h: 2,
    },
  },
  {
    id: 2,
    title: 'Second Widget',
    grid: {
      x: 2,
      y: 0,
      w: 2,
      h: 1,
    },
  },
  {
    id: 3,
    title: 'Third Widget',
    grid: {
      x: 0,
      y: 2,
      w: 2,
      h: 1,
    },
  },
  {
    id: 4,
    title: 'Fourth Widget',
    grid: {
      x: 2,
      y: 2,
      w: 1,
      h: 2,
    },
  },
  {
    id: 5,
    title: 'Fifth Widget',
    grid: {
      x: 3,
      y: 2,
      w: 1,
      h: 2,
    },
  },
])

let grid = null

function initGridStack() {
  grid = GridStack.init({
    column: 4,
    cellHeight: 100,
    minRow: 1,
    margin: 10,
    handle: '.widget-header',
  })
  makeWidgets(widgets.value)
}

function makeWidgets(widgets) {
  widgets.forEach((widget) => {
    makeWidget(widget)
  })
}

function makeWidget(item) {
  const elSelector = `#${item.id}`
  return grid.makeWidget(elSelector)
}

onMounted(() => {
  initGridStack()
})
</script>
