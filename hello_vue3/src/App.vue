<!-- <template> -->
    <!-- 结构 -->
     <!-- html -->
    
    <!-- <Person a="haha" :list="personList" /> -->
<!-- </template> -->

<!-- vue2写法 -->
<!-- <script lang="ts">
    // 交互
    // js 或 ts
    import Person from './components/Person.vue';
    export default {
        name:'App', // 组件名
        components:{Person}  // 注册组件
    }
</script> -->


<!-- <script lang="ts" setup name="App">
    import Person from './components/Person.vue';
    import {reactive} from 'vue'
    import {type Persons } from './types/index.ts';

    let personList= reactive<Persons>([
        {id:'0000001',name:'张三',age:18},
        {id:'0000002',name:'李四',age:20},
        {id:'0000003',name:'王五',age:22},
    ])

    console.log(personList)


</script>
 -->



<template>
    <Person v-if="isShow"/>
</template>


 <script lang="ts" setup name="App">
    import Person from './components/Person.vue';
    import {ref,onMounted} from 'vue'
    
    let isShow = ref(true)


    // 挂载完毕
    onMounted(()=>{
        console.log('父----挂载完毕')
    })

</script>