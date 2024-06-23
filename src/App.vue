<template>
  <div class="container">
    <a-row :gutter="20">
      <VueDraggable
        group="chart"
        v-model="componentsConfig"
        :animation="150"
        ghostClass="ghost"
        class="draggle-block"
        handle=".draggle-handle"
      >
        <draggle-block v-for="item in componentsConfig" :key="item.id">
          <component
            :is="item.component"
          ></component>
        </draggle-block>
      </VueDraggable>
    </a-row>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { VueDraggable } from "vue-draggable-plus";

// import { GridLayout, GridItem } from "grid-layout-plus";
import LineChart from "./components/LineChart.vue";
import BarChart from "./components/BarChart.vue";
import GaugeChart from "./components/GaugeChart.vue";

const componentsConfig = ref([
  {
    id: "LineChart",
    component: LineChart,
  },
  {
    id: "LineChart",
    component: BarChart,
  },
  {
    id: "LineChart",
    component: GaugeChart,
  },
  {
    id: "LineChart",
    component: GaugeChart,
  },
]);
// const layout = reactive([
//   { x: 0, y: 0, w: 3, h: 9, i: "0" },
//   { x: 3, y: 0, w: 3, h: 9, i: "1" },
//   { x: 6, y: 0, w: 3, h: 9, i: "2" },
//   { x: 9, y: 0, w: 3, h: 9, i: "3" },
// ]);
</script>

<style scoped>
.container {
  width: 100%;
  min-height: 100%;
  min-height: 100vh;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.draggle-block {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 100%;
}

.wrapper {
  height: 300px;
}

.vgl-layout {
  background-color: #eee;
}

:deep(.vgl-item:not(.vgl-item--placeholder)) {
  background-color: #ccc;
  border: 1px solid black;
}

:deep(.vgl-item--resizing) {
  opacity: 90%;
}

:deep(.vgl-item--static) {
  background-color: #cce;
}

.text {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  margin: auto;
  font-size: 24px;
  text-align: center;
}

.vgl-item .no-drag {
  width: 100%;
  height: 100%;
}

.vue-draggable-handle {
  position: absolute;
  top: 0;
  right: 0;
  box-sizing: border-box;
  width: 20px;
  height: 20px;
  padding: 0 8px 8px 0;
  cursor: pointer;
  background-color: black;
  background-origin: content-box;
  border-radius: 10px;
}
</style>
