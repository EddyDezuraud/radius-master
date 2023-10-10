<script setup>

import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps({
    modelValue: {
        type: [Number, String],
        default: 0
    },
    label: {
        type: String,
        default: ''
    },
    color: {
        type: String,
        default: '#F6F6F6'
    }
});

const value = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emits('update:modelValue', parseInt(value))
    }
});

const min = 0;
const max = 100;

const emits = defineEmits('change', 'update:modelValue');

const onChange = (e) => {
    emits('change', e)
}

</script>

<template>
    <div :class="$style.wrapper" :style="{ color: color }">
        <div :class="$style.upper">
            <span :class="$style.label">
                {{ label }}
            </span>
            <div :class="$style.counter">
                <button> {{ '-' }} </button>
                <input type="number" @input="onChange" v-model="value" :min="min" :max="max" />
                <button> {{ '+' }} </button>
            </div>
        </div>
        <div :class="$style.rangeWrapper">
            <input type="range" @input="onChange" v-model="value" :min="min" :max="max" />
        </div>
    </div>
</template>

<style module>
.wrapper {
    display: block;
    margin-bottom: 20px;
}

.upper {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.label {
    padding: 4px 6px;
    border-radius: 4px;
    background: rgba(255, 255, 255, .05);
    font-size: 12px;
    font-weight: 700;
    text-shadow: 0 0 15px currentColor;
}

.rangeWrapper {
    display: flex;
    width: 100%;
}

.rangeWrapper input {
    width: 100%;
}

input[type="number"] {
    background: rgba(0, 0, 0, .1);
    padding: 3px 6px;
    border-radius: 2px;
    border: none;
  text-align: center;
  -webkit-appearance: none;
  -moz-appearance: textfield;
  appearance: none;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
    appearance: none;
}

.counter {
    display: flex;
    align-items: center;
}
</style>