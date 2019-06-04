<template>
  <div id="app">
    <button @click="visible = !visible">
      <span v-if="visible"> Hide Config </span>
      <span v-else> Show Config </span>
    </button>
    <div id="container">
      <config
        id="config"
        v-if="visible"
        :items="items"
        @remove-item="handleRemoveItem"
        @add-item="handleAddItem"
      >
      </config>
      <svg xmlns="http://www.w3.org/2000/svg" :view-box.camel="viewbox">
        <g>
          <g v-for="(item, i) in items" :key="item + i">
            <!-- Cubic Bezier Component  -->
            <cubic-bezier
              :index="i"
              :half-size="halfSize"
              :top-height="topHeight"
              :bottom-height="bottomHeight"
              :radius="radius"
              :distance="distance"
              :item="item"
            ></cubic-bezier>
          </g>
        </g>
        <!-- Clipping Mask Component  -->
        <clip-mask
          :title="title"
          :half-size="halfSize"
          :top-height="topHeight"
          :radius="radius"
        ></clip-mask>
      </svg>
    </div>
  </div>
</template>

<script>
import ClipMask from "./components/ClipMask.vue";
import Config from "./components/Config.vue";
import CubicBezier from "./components/CubicBezier.vue";

export default {
  name: "app",
  components: {
    ClipMask,
    Config,
    CubicBezier
  },
  data() {
    return {
      title: "Guardians of the Galaxy",
      size: 1000,
      items: [
        "Starlord",
        "Gamora",
        "Groot",
        "Rocket",
        "Drax",
        "Yondu",
        "Nebula",
        "Korath"
      ],
      visible: false
    };
  },
  computed: {
    topHeight() {
      // 20% of the size
      return this.size * 0.2;
    },
    bottomHeight() {
      // 80% of the size
      return this.size * 0.8;
    },
    width() {
      return this.size;
    },
    halfSize() {
      // 50% of the size
      return this.size * 0.5;
    },
    distance() {
      // distance between two array items on the horizon
      return Math.round(this.width / this.items.length);
    },
    radius() {
      return this.topHeight * 0.5;
    },
    viewbox() {
      return "0 0 " + this.size + " " + this.size;
    }
  },
  methods: {
    handleAddItem(item) {
      this.items.push(item);
    },
    handleRemoveItem(i) {
      this.items.splice(i, 1);
    }
  }
};
</script>

<style>
.item {
  stroke: #ccc;
  stroke-width: 5;
}
path {
  stroke: #5bbaa1;
  fill: none;
  stroke-width: 3;
  stroke-linecap: round;
}
text {
  font-size: 28px;
  text-anchor: middle;
}
#container {
  display: flex;
  height: 100vh;
  justify-content: center;
  border: 2px solid #b2ebf2;
  border-radius: 10px;
}
#config {
  padding: 10px;
  margin: 5px;
  height: fit-content;
  background: #82e5cb;
  border-radius: 5px;
}
svg {
  width: 100%;
  height: 100%;
}

.title {
  font-size: 40px;
}
.clip-svg {
  clip-path: url(#myClip);
}
#config button {
  float: right;
}
.item {
  border-bottom: 1px dashed rgba(0, 0, 0, 0.5);
  padding: 5px;
}
.action {
  padding: 10px;
}
input,
button {
  margin-bottom: 3px;
}
.circle {
  stroke-width: 5;
  stroke: #5bbaa1;
  fill: none;
}
</style>
