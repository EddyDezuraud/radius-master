<script setup>
import { defineProps, computed } from 'vue'

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

const outerStyle = computed(() => {
    return {
        padding: props.padding + 'px',
        borderRadius: props.outer + 'px'
    }
})

const innerStyle = computed(() => {
    return {
        borderRadius: props.inner + 'px'
    }
})
</script>


<template>
    <div>
        <div :class="$style.outer" :style="outerStyle">
            <div :class="$style.inner" :style="innerStyle">

            </div>
        </div>
    </div>
</template>

<style module>
.outer {
    border: solid 1px white;
    width: 500px;
    aspect-ratio: 1;
    box-sizing: border-box;
}

.inner {
    border: solid 1px white;
    width: 100%;
    height: 100%;
}
</style>