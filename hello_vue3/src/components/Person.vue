<!-- <template>
    <div class="person">
        姓：<input type="text"  v-model=firstName><br>
        名：<input type="text" v-model=lastName><br>
        <button @click="changeFullName">将全名改为李四</button><br>
        全名：<span>{{fullName}}</span>
        
    </div>
</template>



<script lang="ts" setup name = 'Person'>
    import {ref,computed} from 'vue'
    let firstName = ref('张')
    let lastName = ref('三')

    // 这样定义的fullName是一个计算属性，且是只读的，无法进行修改
    // let fullName = computed(()=>{
    //     return firstName.value.slice(0,1).toUpperCase() + firstName.value.slice(1) + lastName.value
    // })


    // function changeFullName() {
    //     fullName.value = '李四'
    // }


    // 这样定义的fullName是一个计算属性，可读可写
    let fullName = computed({
        get(){
            return firstName.value.slice(0,1).toUpperCase() + firstName.value.slice(1) + lastName.value

        },
        set(val){
            const [str1,str2] = val.split('-')
            firstName.value = str1
            lastName.value = str2
        }
    })

    function changeFullName() {
        fullName.value = '李-四'
    }
</script> -->



<template>
    <div class="person">
        <h1>情况一：监视【ref】定义的【基本类型】数据</h1>
        <h2>当前求和为：{{ sum }}</h2>
        <button @click="changeSum">点我sum+1</button>
        
    </div>
</template>



<script lang="ts" setup name = 'Person'>
    import {ref,watch} from 'vue'
    // 数据
    let sum = ref(0)

    // 方法
    function changeSum(){
        sum.value += 1
    }

    // 情况一：监视【ref】定义的【基本类型】数据
    const stop = watch(sum,(newvalue,oldvalue)=>{
        console.log('sum变化了',newvalue,oldvalue)
        if(newvalue >= 10){
            stop()
        }
    })

</script>



<style scoped>
    .person {
        background-color: skyblue;
        box-shadow: 0 0 10px;
        border-radius: 10px;
        padding: 20px;
    }

    button {
        margin: 0 5px;
    }
</style>