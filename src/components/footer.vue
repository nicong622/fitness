<script setup>
const emit = defineEmits(['reset', 'run', 'pause'])
</script>

<template>
  <div class="footer">
    <button class="btn" @click="emit('reset')">
      <svg class="reset" >
        <use xlink:href="#refresh" />
      </svg>
    </button>

    <button class="btn" @click="emit('run')">
      <svg class="run" >
        <use xlink:href="#run" />
      </svg>
    </button>

    <button class="btn" @click="emit('pause')">
      <svg class="pause" >
        <use xlink:href="#pause" />
      </svg>
    </button>
  </div>
</template>

<style lang="less" scoped>
.footer {
  display: flex;
  justify-content: space-around;

  svg {
    width: 50px;
    height: 50px;
  }
}
</style>