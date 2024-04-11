<!--  线 + 柱混合图 -->
<template>
  <el-card>
    <template #header>
      <div class="title">TF-IDF词云图</div>
    </template>

    <div :id="id" :class="className" :style="{ height, width }"></div>
  </el-card>
</template>

<script setup lang="ts">
import "echarts-wordcloud";
import * as echarts from "echarts";

const props = defineProps({
  id: {
    type: String,
    default: "wordc",
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

const chart = ref<any>("");

onMounted(() => {
  // 图表初始化
  chart.value = markRaw(
    echarts.init(document.getElementById(props.id) as HTMLDivElement)
  );

  const options = {
    series: [
      {
        type: "wordCloud",
        shape: "circle",
        keepAspect: false,
        // maskImage: maskImage,
        left: "center",
        top: "center",
        width: "100%",
        height: "90%",
        right: null,
        bottom: null,
        sizeRange: [12, 60],
        rotationRange: [-90, 90],
        rotationStep: 45,
        gridSize: 8,
        drawOutOfBound: false,
        layoutAnimation: true,
        textStyle: {
          fontFamily: "sans-serif",
          fontWeight: "bold",
          color: function () {
            return (
              "rgb(" +
              [
                Math.round(Math.random() * 160),
                Math.round(Math.random() * 160),
                Math.round(Math.random() * 160),
              ].join(",") +
              ")"
            );
          },
        },
        emphasis: {
          // focus: 'self',
          textStyle: {
            textShadowBlur: 3,
            textShadowColor: "#333",
          },
        },
        //data属性中的value值却大，权重就却大，展示字体就却大
        data: [
          { name: "bad", value: 1 },
          { name: "behavior", value: 1 },
          { name: "better", value: 1 },
          { name: "care", value: 1 },
          { name: "day", value: 1 },
          { name: "depression", value: 1 },
          { name: "did", value: 1 },
          { name: "doesnt", value: 1 },
          { name: "doing", value: 1 },
          { name: "dont", value: 1 },
          { name: "feel", value: 1 },
          { name: "feeling", value: 1 },
          { name: "friends", value: 1 },
          { name: "going", value: 1 },
          { name: "good", value: 1 },
          { name: "hard", value: 1 },
          { name: "help", value: 1 },
          { name: "hope", value: 1 },
          { name: "hyperactive", value: 1 },
          { name: "im", value: 1 },
          { name: "ive", value: 1 },
          { name: "just", value: 1 },
          { name: "know", value: 1 },
          { name: "life", value: 1 },
          { name: "like", value: 1 },
          { name: "live", value: 1 },
          { name: "lot", value: 1 },
          { name: "love", value: 1 },
          { name: "make", value: 1 },
          { name: "maybe", value: 1 },
          { name: "need", value: 1 },
          { name: "people", value: 1 },
          { name: "person", value: 1 },
          { name: "really", value: 1 },
          { name: "right", value: 1 },
          { name: "say", value: 1 },
          { name: "sure", value: 1 },
          { name: "talk", value: 1 },
          { name: "tell", value: 1 },
          { name: "thats", value: 1 },
          { name: "thing", value: 1 },
          { name: "things", value: 1 },
          { name: "think", value: 1 },
          { name: "time", value: 1 },
          { name: "try", value: 1 },
          { name: "want", value: 1 },
          { name: "way", value: 1 },
          { name: "work", value: 1 },
          { name: "years", value: 1 },
          { name: "youre", value: 1 },
        ],
      },
    ],
  };

  chart.value.setOption(options);

  // 大小自适应
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

<style lang="scss" scoped>
.title {
  display: flex;
  justify-content: space-between;

  .download {
    cursor: pointer;

    &:hover {
      color: #409eff;
    }
  }
}
</style>
