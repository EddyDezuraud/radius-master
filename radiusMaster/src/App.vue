<script setup>
import { ref } from 'vue';

import View from './components/View.vue';
import Sliders from './components/Sliders.vue';

const outer = ref(45);
const inner = ref(10);
const padding = ref(35);

const onChangeOuter = (e) => {
  outer.value = parseInt(e);
  const newVal = parseInt(e) - padding.value;
  inner.value = newVal > 0 ? newVal : 0;
}

const onChangeInner = (e) => {
  inner.value = parseInt(e);
  outer.value = parseInt(e) + padding.value;
}

const onChangePadding = (e) => {
  padding.value = parseInt(e);
  const newVal = outer.value - parseInt(e);
  inner.value = newVal > 0 ? newVal : 0;
}


</script>

<template>
  <div :class="$style.wrapper">
    <header :class="$style.header">
      <div :class=$style.logo>
        <img src="./assets/logo-large.svg" alt="">
      </div>
    </header>
    <View :inner="inner" :padding="padding" :outer="outer" />
    <Sliders :inner="inner" :padding="padding" :outer="outer" @inner="onChangeInner" @outer="onChangeOuter"
      @padding="onChangePadding" />
  </div>
</template>

<style module>
.wrapper {
  display: block;
  padding-top: 70px;
}

.wrapper::before {
  position: absolute;
  content: '';
  width: 1200px;
  aspect-ratio: 1;
  top: -600px;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 50%;
  background: radial-gradient(#8A64DB, #8A64DB00, #8A64DB00);
  opacity: 0.1;
  pointer-events: none;
}

.header {
  position: absolute;
  top: 20px;
  width: 100%;
  left: 0;
  display: flex;
  justify-content: center;
}

.logo {
  display: flex;
  align-content: center;
  gap: 10px;
  font-weight: 700;
}

.logo img {
  height: 35px;
}
</style>