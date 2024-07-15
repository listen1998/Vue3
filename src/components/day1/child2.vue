<template>
    <div> 这里是子组件</div>
    <span>
        <!-- {{ currentInfo.name }}/{{ currentInfo.age }} -->
    </span>
    <span>{{ sss }}</span>
    <el-button size="small" @click="btnClick"> 子组件测试按钮</el-button>
</template>

<script setup>

import { ref, onMounted, watch, computed, watchEffect } from 'vue'

const emit = defineEmits(['inFocus', 'submit', 'input', 'update:modelValue'])

let currentInfo = ref(null)

/**
 *  测试子组件双向绑定, 使用defineModel() 方法
 *  取值直接使用 sss 即可
 *  emit  更新直接操作数据即可
 * 
 *  */


const sss = defineModel('ppppp')

// const props = defineProps(
//     {
//         modelValue: {
//             type: Object,
//             default: () => {
//                 return {}
//             }
//         }
//     }
// )

watchEffect(() => {
    console.log('childWwatchEffect', sss)
    // currentInfo.value = JSON.parse(JSON.stringify(modelValue.value))
})


function btnClick() {
    sss.value.age += 10
}


</script>