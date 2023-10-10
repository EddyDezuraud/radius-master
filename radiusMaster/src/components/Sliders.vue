<script setup>
import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';

import FormInput from './Input.vue';


const localOuter = ref(0);
const localInner = ref(0);
const localPadding = ref(0);

const props = defineProps({
    outer: {
        type: [Number, String],
        default: 0
    },
    inner: {
        type: [Number, String],
        default: 0
    },
    padding: {
        type: [Number, String],
        default: 0
    }
});

const emits = defineEmits('outer', 'inner', 'padding');

const onChange = (name, value) => {
    emits(name, value)
}

onMounted(() => {
    localOuter.value = props.outer;
    localInner.value = props.inner;
    localPadding.value = props.padding;
})

watch(() => props.outer, (newVal) => {
    localOuter.value = newVal;
});

watch(() => props.inner, (newVal) => {
    localInner.value = newVal;
});

watch(() => props.padding, (newVal) => {
    localPadding.value = newVal;
});

</script>


<template>
    <div>
        <FormInput @change="onChange('outer', localOuter)" v-model="localOuter" label="Outer" color="#FF1D53" />
        <FormInput @change="onChange('inner', localInner)" v-model="localInner" label="Inner" color="#9674E2" />
        <FormInput @change="onChange('padding', localPadding)" v-model="localPadding" label="Padding" color="#96FF43" />
    </div>
</template>