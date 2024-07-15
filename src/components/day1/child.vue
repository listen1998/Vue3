<template>
    <div> 这里是子组件</div>
    <span>
        {{ currentInfo.name }}/{{ currentInfo.age }}
    </span>
    <el-button size="small" @click="btnClick"> 子组件测试按钮</el-button>
</template>

<script setup>

import { ref, onMounted, watch, computed, watchEffect } from 'vue'

const emit = defineEmits(['inFocus', 'submit', 'input', 'update:modelValue'])

let currentInfo = ref(null)

const props = defineProps(
    {
        modelValue: {
            type: Object,
            default: () => {
                return {}
            }
        }
    }
)

watchEffect(() => {
    console.log('childWwatchEffect', props.modelValue)
    currentInfo.value = JSON.parse(JSON.stringify(props.modelValue))
})


function btnClick() {
    currentInfo.value.age++
    emit('update:modelValue', currentInfo.value)
}


</script>