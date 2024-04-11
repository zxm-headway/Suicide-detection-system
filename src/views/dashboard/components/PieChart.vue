<!-- 饼图 -->
<template>
  <el-card>
    <template #header> 自杀风险分类饼图 </template>
    <div :id="id" :class="className" :style="{ height, width }"></div>
  </el-card>
</template>

<script setup lang="ts">
import * as echarts from "echarts";

const props = defineProps({
  id: {
    type: String,
    default: "pieChart",
  },
  className: {
    type: String,
    default: "",
  },
  width: {
    type: String,
    default: "200px",
    required: true,
  },
  height: {
    type: String,
    default: "200px",
    required: true,
  },
});
const options = {
  grid: {
    left: "2%",
    right: "2%",
    bottom: "10%",
    containLabel: true,
  },
  legend: {
    top: "bottom",
    textStyle: {
      color: "#999",
    },
  },
  series: [
    {
      name: "Nightingale Chart",
      type: "pie",
      radius: [30, 100],
      center: ["50%", "50%"],
      roseType: "area",

      itemStyle: {
        borderRadius: 1,
        color: function (params: any) {
          //自定义颜色
          const colorList = [
            "#409EFF",
            "#67C23A",
            "#E6A23C",
            "#F56C6C",
            "#909399",
          ];
          return colorList[params.dataIndex];
        },
      },
      data: [
        { value: 108, name: "Supportive" },
        { value: 99, name: "Indicator" },
        { value: 171, name: "Ideation" },
        { value: 77, name: "Behavior" },
        { value: 45, name: "Attempt" },
      ],
    },
  ],
  tooltip: {
    trigger: "item",
  },
};

const chart = ref<any>("");

onMounted(() => {
  chart.value = markRaw(
    echarts.init(document.getElementById(props.id) as HTMLDivElement)
  );

  chart.value.setOption(options);

  window.addEventListener("resize", () => {
    chart.value.resize();
  });
});

onActivated(() => {
  if (chart.value) {
    chart.value.resize();
  }
});
</script>
