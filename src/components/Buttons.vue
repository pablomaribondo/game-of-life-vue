<template>
  <div class="center">
    <div>
      <b-button-toolbar>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('play')"
          :disabled="state === 'running'"
        >
          Play
        </b-button>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('pause')"
          :disabled="state === 'paused' || state === 'stopped'"
        >
          Pause
        </b-button>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('clear')"
          :disabled="state === 'stopped'"
        >
          Clear
        </b-button>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('slow')"
          :disabled="state === 'paused' || state === 'stopped'"
        >
          Slow
        </b-button>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('fast')"
          :disabled="state === 'paused' || state === 'stopped'"
        >
          Fast
        </b-button>
        <b-button
          class="tbar-btn"
          variant="outline-light"
          @click="$emit('seed')"
        >
          Seed
        </b-button>
        <b-dropdown
          text="Grid Size"
          class="tbar-btn"
          variant="outline-light"
          :disabled="state === 'running'"
        >
          <b-dropdown-item-button @click="$emit('gridSize', $event.target.innerText)">
            20x10
          </b-dropdown-item-button>
          <b-dropdown-item-button @click="$emit('gridSize', $event.target.innerText)">
            50x30
          </b-dropdown-item-button>
          <b-dropdown-item-button @click="$emit('gridSize', $event.target.innerText)">
            70x50
          </b-dropdown-item-button>
        </b-dropdown>
      </b-button-toolbar>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Buttons',
  props: {
    state: String,
  },
};
</script>

<style lang="scss" scoped>
.center {
  margin: auto;
  display: table;
  margin-top: 10px;
}

.tbar-btn {
  margin: 0 5px;
}
</style>
