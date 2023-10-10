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
    <div :class="$style.wrapper">
        <div :class="$style.upper">
            <span>
                {{ label }}
            </span>
            <input type="number" @input="onChange" v-model="value" :min="min" :max="max" />
        </div>
        <div :class="$style.rangeWrapper">
            <input type="range" @input="onChange" v-model="value" :min="min" :max="max" />
        </div>
    </div>
</template>

<style module>
.wrapper {
    display: block;
}

.upper {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>