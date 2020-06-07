<template>
  <div
    :class="boxClass"
    :id="boxId"
    @click="$emit('selectBox')"
  />
</template>

<script>
export default {
  name: 'Box',
  props: {
    boxClass: String,
    boxId: String,
  },
};
</script>

<style lang="scss" scoped>
.box {
  display: inline-block;
  border: 1px solid transparent;
  border-radius: 10%;
  width: 15px;
  height: 15px;
  margin-left: -1px;
  margin-bottom: -1px;
  cursor: pointer;

  &:hover {
    background: #ca7aff;
  }
}
.on {
  background-color: #ff7f50;
}

.off {
  background-color: transparent;
}
</style>
