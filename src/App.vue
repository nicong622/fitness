<script setup>
  import { onMounted, ref } from 'vue';
  import SvgIcon from './components/icons.vue';
  import Countdown from './components/countdown.vue';
  import Footer from './components/footer.vue';
  import { STATUS_ENUM } from './constants/index';

  const tasksList = ref([5, 2, 5, 2, 5, 2, 5, 2, 5, 2, 5, 2, 5, 2, 5, 2]);
  const activeIndex = ref(-1);
  const status = ref(STATUS_ENUM.PENGING);

  function onTimeout() {
    if (activeIndex.value < tasksList.value.length) {
      activeIndex.value += 1;
    }
  }

  function reset() {
    activeIndex.value = 0;
    status.value = STATUS_ENUM.RESET;
  }

  function pause() {
    status.value = STATUS_ENUM.PAUSED
  }

  function run() {
    status.value = STATUS_ENUM.RUNNING
  }

  onMounted(() => {
    activeIndex.value = 0;
  });
</script>

<template>
  <SvgIcon />

<div class="container">
  <div class="countdown-group">
  <Countdown
    v-for="(item, index) in tasksList"
    :key="item"
    :seconds="item"
    :is-active="activeIndex === index"
    :status="status"
    @timeout="onTimeout"
  />
  </div>

  <Footer
    class="footer"
    @reset="reset"
    @pause="pause"
    @run="run"
  />
  </div>
</template>

<style lang="less" scoped>
  .container {
    height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .countdown-group {
    flex: 1;
    overflow: auto;
  }

  .footer {
    padding: 16px 0;
    border-top: 1px solid #ccc;
  }
</style>

<style lang="less">
 body,
  div,
  button,
  p {
    padding: 0;
    margin: 0;
  }

  button {
    background-color: transparent;
    border: none;
  }
</style>