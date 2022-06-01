<script setup>
import { ref, watch } from 'vue';
import { STATUS_ENUM } from '../constants/index';

const props = defineProps({
  seconds: Number,
  isActive: Boolean,
  status: String
})

const timeLeft = ref(props.seconds)

const emit = defineEmits(['timeout'])

let timer = null;

function run() {
  if (timeLeft.value > 0) {
    timer = setTimeout(() => {
      timeLeft.value--
      run()
    }, 1000)
  } else {
    emit('timeout')
    clearTimeout(timer)
  }
}

watch(() => props.isActive, (isActive) => {
  if (isActive) {
    run()
  } else {
    clearTimeout(timer)
    timeLeft.value = props.seconds
  }
})

watch(() => props.status, (status) => {
  if (props.isActive && status === STATUS_ENUM.PAUSED) {
    clearTimeout(timer)
  } else if (props.isActive && status === STATUS_ENUM.RUNNING) {
    run()
  }
})
</script>

<template>
  <div class="count-down" :class="{ active: isActive }">
    <p>{{ timeLeft }}</p>
  </div>
</template>

<style lang="less" scoped>
.count-down {
  font-size: 10px;
  text-align: center;
  padding: 1em 0;
  transition: all 0.1s;

  p {
    font-size: 3em;
    color: #999;
  }


  &.active {
    padding: 1.5em 0;
    background-color: #92B4EC;

    p {
      font-size: 5em;
      color: #fff;
    }
  }
}
</style>