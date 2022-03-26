<template>
  <div id="app">
    <div v-if="loaded" class="board w-full p-4">
      <div class="row flex bg-green-400">
        <div class="w-8"></div>
        <div
          v-for="col in cols"
          :key="col"
          class="flex flex-grow justify-center"
        >
          {{ String.fromCharCode(64 + col) }}
        </div>
      </div>
      <div v-for="row in rows" :key="row" class="flex">
        <div class="w-8 text-center bg-green-400">{{ row }}</div>
        <div v-for="col in cols" :key="col" class="flex flex-grow bg-green-400">
          <Cell
            :x="col"
            :y="row"
            :value="matrix[row - 1][col - 1]"
            :rows="rows"
            :cols="cols"
            :selected="row == cy && col == cx"
            @select="(x, y) => select(x || col, y || row)"
            @update="update"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Cell from "./components/Cell";

export default {
  name: "App",
  components: {
    Cell,
  },
  data() {
    return {
      rows: 5,
      cols: 5,
      cx: 1,
      cy: 2,
      matrix: null,
      loaded: false,
    };
  },
  mounted() {
    this.matrix = Array.from({ length: this.rows }, () =>
      new Array(this.cols).fill("")
    );
    this.loaded = true;
  },
  methods: {
    select(col, row) {
      this.cx = col;
      this.cy = row;
    },
    update(x, y, val) {
      this.matrix[y - 1][x - 1] = val;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/** Common Styles **/
</style>
