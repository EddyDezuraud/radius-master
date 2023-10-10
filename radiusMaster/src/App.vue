<script setup>
import { ref } from 'vue';

import View from './components/View.vue';
import Sliders from './components/Sliders.vue';

const inner = ref(0);
const outer = ref(0);
const padding = ref(0);

const onChangeOuter = (e) => {
  outer.value = parseInt(e);
  inner.value = parseInt(e) - padding.value;
}

const onChangeInner = (e) => {
  inner.value = parseInt(e);
  outer.value = parseInt(e) + padding.value;
}

const onChangePadding = (e) => {
  padding.value = parseInt(e);
  inner.value = outer.value - parseInt(e);
}


</script>

<template>
  <div>
    <View :inner="inner" :padding="padding" :outer="outer" />
    <Sliders :inner="inner" :padding="padding" :outer="outer" @inner="onChangeInner" @outer="onChangeOuter"
      @padding="onChangePadding" />
  </div>
</template>

<style module></style>
