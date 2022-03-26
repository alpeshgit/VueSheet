<template>
  <div class="">
    <input
      type="text"
      class="w-full outline-none focus:bg-gray-200 border border-gray-200 focus:border-gray-600"
      :class="{ 'bg-gray-200': selected }"
      :value="value"
      @input="$emit('update', x, y, $event.target.value)"
      ref="self"
      @click="$emit('select')"
      v-on:keyup.enter="$emit('select', x, Math.min(y + 1, rows))"
      v-on:keyup.up="$emit('select', x, y - 1 || 1)"
      v-on:keyup.down="$emit('select', x, Math.min(y + 1, rows))"
      v-on:keyup.tab="
        $event.shiftKey
          ? $emit('select', x, y)
          : $emit('select', Math.min(x, cols), y)
      "
    />
  </div>
</template>

<script>
export default {
  name: "Cell",
  props: {
    x: Number,
    y: Number,
    cols: Number,
    rows: Number,
    value: String,
    selected: Boolean,
  },
  emits: ["select", "update"],
  data() {
    return {};
  },
  watch: {
    selected: function (newVal, oldVal) {
      let el = this.$refs.self;
      if (newVal)
        this.$nextTick(function () {
          el.focus();
        });
    },
  },
  mounted() {
    //this.$refs.self.focus();
  },
};
</script>

<style scoped>
</style>