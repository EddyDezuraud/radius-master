<script setup>
import { onMounted, ref } from 'vue';

import View from './components/View.vue';
import Sliders from './components/Sliders.vue';
import Onboarding from './components/Onboarding.vue';

const outer = ref(65);
const inner = ref(30);
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

const showOnboarding = ref(true);

onMounted(() => {
  window.setTimeout(() => {
    showOnboarding.value = false;
  }, 2500)
})

</script>

<template>
  <div :class="$style.wrapper">
    <Onboarding v-if="showOnboarding" />
    <div v-else :class="$style.inner">
      <header :class="$style.header">
        <div :class=$style.logo>
          <img src="./assets/logo-large.svg" alt="">
        </div>
      </header>
      <View :class="$style.view" :inner="inner" :padding="padding" :outer="outer" />
      <Sliders :class="$style.sliders" :inner="inner" :padding="padding" :outer="outer" @inner="onChangeInner" @outer="onChangeOuter"
        @padding="onChangePadding" />
    </div>

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

.inner {
  display: flex;
  align-items: center;
  gap: 40px;
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

.logo,
.view,
.sliders {
  animation: botEltsAppearing 0.6s ease;
}

.view {
  animation-fill-mode: backwards;
  animation-delay: 0.3s;
}

.sliders {
  animation-fill-mode: backwards;
  animation-delay: 0.4s;
}

.logo img {
  height: 35px;
}

@media screen and (max-width: 1000px) {
  .inner {
    flex-direction: column;
  }
}

@keyframes topLogoAppearing {
    0% {
        opacity: 0;
        transform: translateY(-10px);
    }

    90% {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes botEltsAppearing {
    0% {
        opacity: 0;
        transform: translateY(20px);
    }

    90% {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>