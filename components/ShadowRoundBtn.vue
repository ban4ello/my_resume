<template>
  <div class="text-title shadow-round-btn" @click="$emit('click')">
    <span :style="{ color: textColor }">{{ btnText }}</span>
  </div>
</template>
<script>
export default {
  props: {
    btnText: {
      type: String,
      default: ''
    },

    textColor: {
      type: String,
      default: '#fff'
    }
  }
}
</script>
<style lang="scss" scoped>
.shadow-round-btn {
  height: 48px;
  width: 300px;
  padding: 15px 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(45deg, black, transparent);
  border: 1px #000 solid;
  border-radius: 25px;
  box-shadow: 4px 6px 11px;
  color: #000;
  cursor: pointer;

  &:hover {
    box-shadow: 2px 4px 8px;
  }

  &.disabled {
    cursor: not-allowed;
  }
}
</style>
