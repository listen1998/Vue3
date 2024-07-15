<template>
    <el-input ref="customInput" v-model="target.age" />
    <span> 当前用户名：{{ target.name }} </span>
    <span> 当前用户年龄:{{ target.age }}</span>

    <div :class="{ 'age-18': target.age >= 18 }">
        {{ currentInfo }}
    </div>

    <div v-if="target.age > 18">
        条件命中
    </div>
    <el-select v-model="target.name" placeholder="请选择">
        <el-option v-for="item in arrList" :key="item.id" :label="item.name" :value="item.name" />
    </el-select>
    <el-button @click="test">测试按钮</el-button>
    <children2 v-model:ppppp="target" />
</template>


<script setup>
import { ref, onMounted, watch, computed, watchEffect } from 'vue'
import { ElMessage } from 'element-plus'
import children from './child.vue'
import children2 from './child2.vue'
const target = ref({
    name: 'test',
    age: 0
})

const customInput = ref(null)
const tempValue = ref(0)
// 这里测试 v-for
const arrList = ref([])
//  这里测试Mounted 生命周期
onMounted(() => {
    ElMessage.success('这里测试 mounted事件')
    setTimeout(() => {
        arrList.value = [
            { id: 1, name: 'User 1' },
            { id: 2, name: 'User 2' },
            { id: 3, name: 'User 3' },
            { id: 4, name: 'User 4' },
            { id: 5, name: 'User 5' },
            { id: 6, name: 'User 6' },
            { id: 7, name: 'User 7' },
            { id: 8, name: 'User 8' },
            { id: 9, name: 'User 9' },
            { id: 10, name: 'User 10' }
        ]

    }, 0);
    tempValue.value = 100
    //  这里测试ref 引用
    customInput.value.focus()
    console.log('mounted', customInput)
})
//  这里测试 change 事件  这里直接监听 target.value.age不生效*/

// watch(target.value.age, (newValue, oldValue) => {
//     ElMessage.info(`当前 tempValue:${newValue}`)
//     console.log('watch', newValue)
// }, {
//     immediate: true
// })
//  这里测试 change 事件,使用 getter 函数形式生效 */
watch(() => target.value.age, (newValue, oldValue) => {
    ElMessage.info(`当前 tempValue:${newValue}`)
    console.log('watch', newValue)
}, {
    immediate: true
})
//  这里测试 watchEffect 事件
watchEffect(() => {
    console.log('watchEffect', target.value.age)
})


// 这里测试计算属性
const currentInfo = computed(() => {
    return `当前用户名：${target.value.name} 当前用户年龄:${target.value.age}`
})

function test(params) {
    target.value.age++
}


function childrenInputEmit(params) {
    console.log('childrenInputEmit', params)
    target.value = JSON.parse(JSON.stringify(params))
}

</script>
<style scoped>
/**
 这里测试动态 class
 */
.age-18 {
    color: green;
    background: lightblue;
}
</style>