<template>
  <div>
    <h2>图表</h2>
    <div class="chart" id="oneChart">图标容器</div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    // 引入echarts
    let $echarts = inject("echarts");
    let $http = inject("axios");
    // 数据接收
    let oneData = reactive({});
    let xData = reactive([]);
    let yData = reactive([]);
    function setData() {
      xData = oneData.data.chartOne.chartData.map((v) => v.title);
      yData = oneData.data.chartOne.chartData.map((v) => v.num);
      console.log(xData);
      console.log(yData);
    }
    async function getState() {
      oneData = await $http({ url: "/one/data" });
      // console.log(oneData.data.chartOne.chartData);
    }
    onMounted(() => {
      // 初始化echarts
      let myChart = $echarts.init(document.getElementById("oneChart"));
      getState().then(() => {
        setData();
        myChart.setOption({
          gird: {
            left: "20",
            containLabel: true,
          },
          // 设置柱状图
          xAxis: {
            type: "value",
            axisLabel: {
              show: true,
              textStyle: {
                color: "#fff",
              },
            },
          },
          yAxis: {
            type: "category",
            data: xData,
            axisLabel: {
              show: true,
              textStyle: {
                color: "#fff",
              },
            },
          },
          series: [
            {
              // 样式设置
              itemStyle: {
                normal: {
                  barBorderRadius: [0, 10, 10, 0],
                  color: new $echarts.graphic.LinearGradient(0, 0, 1, 0, [
                    {
                      offset: 0,
                      color: "#005eaa",
                    },
                    {
                      offset: 0.5,
                      color: "#339ca8",
                    },
                    {
                      offset: 1,
                      color: "#cda819",
                    },
                  ]),
                },
              },
              data: yData,
              type: "bar",
            },
          ],
        });
        window.onresize = myChart.resize;
      });
    });
    return {
      getState,
      oneData,
      xData,
      yData,
      setData,
    };
  },
};
</script>

<style lang="less" scoped>
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