<template>
  <div>
    <apexchart :options="chartOptions" :series="chartData" type="bar" height="200" width=600></apexchart>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import VueApexCharts from 'vue3-apexcharts';
import ApexCharts from 'apexcharts';

export default {
  components: {
    apexchart: VueApexCharts,
  },
  setup() {
    const chartOptions = ref({
      chart: {
        id: 'basic-bar',
      },
      xaxis: {
        categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      },
    });

    const chartData = ref([
      {
        name: 'Series 1',
        data: [30, 40, 45, 50, 49, 60, 70, 91, 125, 135, 152, 170],
      },
    ]);

    onMounted(() => {
      const chart = new ApexCharts(document.querySelector('#chart'), {
        options: chartOptions.value,
        series: chartData.value,
        type: 'bar',
        height: 400,
      });
      chart.render();
    });

    return { chartOptions, chartData };
  },
};
</script>
