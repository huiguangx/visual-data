<template>
  <div>
    <h2>库存统计图</h2>
    <div class="chart" id="fourChart"></div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");
    let fourData = reactive({});
    async function getState() {
      fourData = await $http({ url: "/four/data" });
    }
    onMounted(() => {
      getState().then(() => {
        let myChart = $echarts.init(document.getElementById("fourChart"));
        myChart.setOption({
          grid: {
            left: "3%",
            right: "4%",
            bottom: "3%",
            containLabel: true,
          },
          xAxis: {
            type: "category",
            data: fourData.data.chartFour.chartData.day,
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          yAxis: {
            type: "value",
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "shadow",
            },
          },
          legend: {},
          series: [
            {
              name: "服饰",
              type: "bar",
              data: fourData.data.chartFour.chartData.num.Clothes,
              // 柱状图堆叠
              stack: "Total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
            },
            {
              name: "数码产品",
              type: "bar",
              data: fourData.data.chartFour.chartData.num.digit,
              // 柱状图堆叠
              stack: "Total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
            },
            {
              name: "家电",
              type: "bar",
              data: fourData.data.chartFour.chartData.num.Electrical,
              // 柱状图堆叠
              stack: "Total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
            },
            {
              name: "家居",
              type: "bar",
              data: fourData.data.chartFour.chartData.num.gear,
              // 柱状图堆叠
              stack: "Total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
            },
            {
              name: "日化",
              type: "bar",
              data: fourData.data.chartFour.chartData.num.Chemicals,
              // 柱状图堆叠
              stack: "Total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
            },
          ],
        });
      });
    });
  },
};
</script>

<style scoped>
.chart {
  height: 4.5rem;
}
h2 {
  height: 0.6rem;
  color: #fff;
  line-height: 0.6rem;
  text-align: center;
}
</style>