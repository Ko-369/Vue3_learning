<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄：{{ age }}</h2>
         <button @click="changeName">修改名字</button>
         <button @click="changeAge">修改年龄</button>
         <button @click="showTel">查看联系方式</button>
    </div>
</template>


<script lang="ts">
    export default {
        name:'Person',
        // 选项式（配置式）API ===> vue2 写法 
        // data() {
        //     return {
        //         name:'张三',
        //         age:18,
        //         tel:'13888888888'
        //     }
        // },
        // methods:{
        //     showTel(){
        //         alert(this.tel)
        //     },

        //     changeName(){
        //         this.name = 'zhang-san'
        //     },


        //     changeAge(){
        //         this.age += 1
        //     }
        // },
        
        
        
        // 组合式API ====> vue3 写法
        setup() {
            // 数据
            let name = '张三'  // 注意：此时的name，age，tel都不是响应式的，所以在页面无法改变成功
            let age = 18
            let tel = '13888888888'


            // 方法
            function changeName(){
                name = 'zhang-san'
            }

            function changeAge(){
                age += 1
            }

            function showTel(){
                alert (tel)
            }

            return {name,age,changeName,changeAge,showTel}
        }
    }
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