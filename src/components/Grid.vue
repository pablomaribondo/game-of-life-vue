<template>
  <div v-if="cols && rows" class="grid" :style="{width: `${width}px`}">
    <Box
      v-for="element in gridElementsList"
      :key="element.boxId"
      :boxClass="element.boxClass"
      :boxId="element.boxId"
      @selectBox="$emit('selectBox', {col: element.col, row: element.row})"
    />
  </div>
</template>

<script>
import Box from '@/components/Box.vue';

export default {
  name: 'Grid',

  components: {
    Box,
  },

  props: {
    cols: Number,
    rows: Number,
    fullGrid: Array,
  },

  computed: {
    width() {
      return this.cols * 14;
    },

    gridElementsList() {
      const gridElements = [];
      let boxClass = '';
      for (let i = 0; i < this.rows; i += 1) {
        for (let j = 0; j < this.cols; j += 1) {
          const boxId = `${i}_${j}`;
          boxClass = this.fullGrid[i][j] ? 'box on' : 'box off';
          gridElements.push({
            boxClass,
            boxId,
            row: i,
            col: j,
          });
        }
      }

      return gridElements;
    },
  },
};
</script>

<style lang="scss" scoped>
.grid {
  width: 150px;
  line-height: 0;
  margin: auto;
  box-shadow: 0px 0px 20px #f0f0f0;
  margin-top: 20px;
  border-radius: 1%;
}
</style>
