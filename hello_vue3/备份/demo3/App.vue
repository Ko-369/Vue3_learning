<template>
    <!-- 结构 -->
    <!-- html -->

    <Person/>

</template>

<script lang="ts">
    // 交互
    // js 或 ts
    import Person from './components/Person.vue';
    export default {
        name:'App', // 组件名
        components:{Person}  // 注册组件
    }
</script>


