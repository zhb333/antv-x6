<script setup lang="ts">
import { Graph } from "@antv/x6";
import { ref, onMounted } from "vue";
const container = ref<HTMLElement | null>(null);
const data = {
  // 节点
  nodes: [
    {
      id: "node1",
      shape: "rect", // 使用 rect 渲染
      x: 100,
      y: 200,
      width: 80,
      height: 40,
      label: "hello",
    },
    {
      id: "node2",
      shape: "ellipse", // 使用 ellipse 渲染
      x: 300,
      y: 200,
      width: 80,
      height: 40,
      label: "world",
    },
  ],
  // 边
  edges: [
    {
      source: "node1", // String，必须，起始节点 id
      target: "node2", // String，必须，目标节点 id
    },
  ],
};

onMounted(() => {
  if (!container.value) return;
  const graph = new Graph({
    container: container.value,
    width: 800,
    height: 600,
    background: {
      color: "#fffbe6", // 设置画布背景颜色
      image: "https://sponsors.vuejs.org/images/dcloud.avif",
      position: "center",
      size: {
        width: 200,
        height: 100,
      },
      repeat: "watermark",
      opacity: 1,
      quality: 1,
      angle: 30,
    },
    grid: {
      size: 10, // 网格大小 10px
      visible: true, // 渲染网格背景
      type: "doubleMesh", // 'dot' | 'fixedDot' | 'mesh'
      args: [
        {
          color: "#eee", // 主网格线颜色
          thickness: 1, // 主网格线宽度
        },
        {
          color: "#ddd", // 次网格线颜色
          thickness: 1, // 次网格线宽度
          factor: 4, // 主次网格线间隔
        },
      ],
    },
  });

  graph.fromJSON(data);

  // setTimeout(() => {
  // graph.drawBackground({
  //   color: "#f5f5f5",
  // });
  // }, 1000);

  // setTimeout(() => {
  //   graph.updateBackground();
  // }, 1000);

  // setTimeout(() => {
  //   graph.clearBackground();
  // }, 1000);
  console.log(graph.getGridSize());
  graph.setGridSize(20);
  // graph.zoom(0);
  graph.translate(80, 40);
});
</script>

<template>
  <main>
    <div ref="container"></div>
  </main>
</template>
