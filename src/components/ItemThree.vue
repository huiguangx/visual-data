<template>
  <div>
    <h2>库存统计</h2>
    <div class="chart" id="threeChart"></div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";

export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");
    let threeData = reactive({});
    async function getState() {
      threeData = await $http({ url: "/three/data" });
    }
    onMounted(() => {
      getState().then(() => {
        console.log("饼状图", threeData.data.chartThree.chartData);
        let myChart = $echarts.init(document.getElementById("threeChart"));
        myChart.setOption({
          // 设置图例
          legend: {
            top: "bottom",
          },
          // 提示框
          tooltip: {
            show: true,
          },
          series: [
            {
              type: "pie", // 类型为饼状图
              data: threeData.data.chartThree.chartData,
              radius: [10, 100],
              center: ["50%", "45%"],
              roseType: "area",
              itemStyle: {
                borderRadius: 10,
              },
            },
          ],
        });
        // echarts自适应
        window.onresize = myChart.resize;
      });
    });
    return {
      getState,
      threeData,
    };
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