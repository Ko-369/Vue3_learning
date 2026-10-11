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



<!-- <template>
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

</script> -->


<!-- <template>
    <div class="person">
        <h1>情况二：监视【ref】定义的【对象类型】数据</h1>
        <h2>姓名：{{ person.name}}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <button @click="changeAge">修改年龄</button>
        <button @click="changeName">修改名字</button>
        <button @click="changePerson">修改整个人</button>




    </div>




</template>


<script lang = 'ts' setup name = 'Person'>
    import {ref,watch} from 'vue'

    // 数据
    let person = ref({
        name:'张三',
        age:18
    })

    // 方法
    function changeAge(){
        person.value.age += 1
    }

    function changeName(){
        person.value.name += '~'
    }

    function changePerson(){
        person.value = {name:'李四',age:90}

    }

    // 监视，情况二：监视【ref】定义的【对象类型】数据，监视的是对象的地址值，若想监视对象内部属性的变化，需要手动开启深度监视
    // watch 的第一个参数是：被监视的数据
    // watch 的第二个参数是：监视的回调
    // watch 的第三个参数是：配置对象(deep、immediate等等)
    watch(person,(newvalue,oldvalue)=>{
        console.log('person变化了')
    },{deep:true})



</script> -->

<!-- <template>
    <div class="person">
        <h1>情况三：监视【reactive】定义的【对象类型】数据</h1>
        <h2>姓名：{{ person.name}}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <button @click="changeAge">修改年龄</button>
        <button @click="changeName">修改名字</button>
        <button @click="changePerson">修改整个人</button>

    </div>

</template>


<script lang="ts" setup name = 'person'>
    import {reactive,watch} from 'vue'

    // 数据
    let person = reactive({
        name:'张三',
        age:18
    })

    // 方法
    function changeAge(){
        person.age += 1
    }

    function changeName(){
        person.name += '~'
    }

    function changePerson(){
        Object.assign(person,{name:'李四',age:80})

    }
    // 监视，情况三：监视【reactive】定义的【对象类型】数据，且默认是开启深度监视的
    watch(person,(newvalue,oldvalue)=>{
        console.log('person变化了',newvalue,oldvalue)
    })




</script> -->


<!-- <template>
    <div class="person">
        <h1>情况四：监视响应式对象中的某个属性</h2>
        <h2>姓名：{{ person.name }}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <h2>汽车：{{ person.car.c1}}、{{ person.car.c2 }}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="C1">修改第一台车</button>
        <button @click="C2">修改第二台车</button>
        <button @click="changeCar">修改所有车</button>




    </div>

</template>


<script lang="ts" setup name = 'person'>
    import {reactive,watch} from 'vue'

    // 数据
    let person = reactive({
        name:'张三',
        age:18,
        car:{
            c1:'奔驰',
            c2:'宝马'
        }
    })

    // 方法
    function changeName(){
        person.name += '~'
    }

    function changeAge(){
        person.age += 1
    }

    function C1(){
        person.car.c1 = '奥迪'
    }

    function C2(){
        person.car.c2 = '大众'
    }

    function changeCar(){
        person.car = {c1:'雅迪',c2:'爱玛'}
    }

    // 监视，情况四：监视响应式对象中的某个属性，且该属性是基本类型的，要写成函数式
    // watch(()=>person.name,(newvalue,oldvalue)=>{
    //     console.log('person变化了',newvalue,oldvalue)
    // })

    // 监视，情况四：监视响应式对象中的某个属性，且该属性是对象类型的，可以直接，但最好写成函数式
    watch(()=>person.car,(newvalue,oldvalue)=>{
        console.log('person.car发生变化了',newvalue,oldvalue)
    },{deep:true})

</script> -->



<!-- <template>
    <div class="person">
        <h1>情况五：监视上述的多个数据</h1>
        <h2>姓名：{{ person.name }}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <h2>汽车：{{ person.car.c1}}、{{ person.car.c2 }}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="C1">修改第一台车</button>
        <button @click="C2">修改第二台车</button>
        <button @click="changeCar">修改所有车</button>




    </div>

</template>


<script lang="ts" setup name = 'person'>
    import {reactive,watch} from 'vue'

    // 数据
    let person = reactive({
        name:'张三',
        age:18,
        car:{
            c1:'奔驰',
            c2:'宝马'
        }
    })

    // 方法
    function changeName(){
        person.name += '~'
    }

    function changeAge(){
        person.age += 1
    }

    function C1(){
        person.car.c1 = '奥迪'
    }

    function C2(){
        person.car.c2 = '大众'
    }

    function changeCar(){
        person.car = {c1:'雅迪',c2:'爱玛'}
    }

  

    // 监视，情况五：监视上述的多个数据
    watch([()=>person.name,person.car],(newvalue,oldvalue)=>{
        console.log('person.car发生变化了',newvalue,oldvalue)
    },{deep:true})

</script> -->



<!-- <template>
    <div class="person">
        <h2>需求：当水温达到60度，或水位达到80cm时，给服务器发请求</h2>
        <h2>当前水温：{{ temp }}</h2>
        <h2>当前水位：{{ height}}</h2>
        <button @click="changeTemp">点我水温+10</button>
        <button @click="changeHeight">点我水位+10</button>


    </div>

</template>


<script lang = "ts" setup name = "person">
    import {ref,watch,watchEffect} from 'vue'

    // 数据
    let temp = ref(10)
    let height = ref(0)


    // 方法
    function changeTemp(){
        temp.value += 10
    }

    function changeHeight(){
        height.value += 10
    }

    // 监视 ---- watch 实现
    // watch([temp,height],(value)=>{
    //     let [newTemp,newHeight] = value
    //     if(newTemp >= 60 || newHeight >=80){
    //         console.log('给服务器发请求')
    //     }
    // })


    
   // 监视 ------ watchEffect 实现
    // watchEffect(()=>{
    //     if(temp.value >= 60 || height.value >= 80){
    //         console.log('给服务器发请求')
    //     }
    // })

</script> -->


<!-- <template>
    <div class="person">
        <h1>中国</h1>
        <h2 ref="title2">北京</h2>
        <h3>尚硅谷</h3>
        <button @click="showLog">点我输出h2这个元素</button>




    </div>
</template>

<script lang="ts" setup name = "person">
    import {ref} from 'vue'


    // 创建title2容器，用于存储ref标记的内容
    let title2 = ref()


    function showLog(){
        console.log(title2.value)
    }



</script> -->


<!-- <template>
    <div class="person">
        



    </div>
</template>

<script lang="ts" setup name="Person">
    import {type PersonInter,type Persons } from '@/types'

    // let person:PersonInter = {id:'00000001',name:'张三',age:60}

    let personList:Persons = [
        {id:'00000001',name:'张三',age:60},
        {id:'00000002',name:'李四',age:18},
        {id:'00000003',name:'王五',age:5}
    ]


</script> -->


<!-- <template>
    <div class="person">
        <ul>
            <li v-for="item in list" :key="item.id">
                {{ item.name }} -- {{ item.age }}
            </li>
        </ul>


    </div>
</template>


<script lang="ts" setup name="Person">
    import { withDefaults } from 'vue'
    import {type Persons } from '@/types'

    // 只接收list
    // defineProps(['list'])


    // 接收list + 限制类型
    // defineProps<{list:Persons}>()

    // 接收list + 限制类型 + 限制必要性 +指定默认值
    withDefaults(defineProps<{list?:Persons}>(),{
        list:()=>[{id:'0000005',name:'康师傅1',age:19}]
    })



    // 接收list，同时将props保存起来
    // let x = defineProps(['list'])
    // console.log(x.list)

</script> -->


<template>
    <div class="person">
        <h2>当前求和为：{{ sum }}</h2>
        <button @click="add">点我sum+1</button>


    </div>

</template>


<script lang="ts" setup name="Person">
    import {ref, onBeforeMount,onMounted,onBeforeUpdate,onUpdated,onBeforeUnmount,onUnmounted} from 'vue'

    // 数据
    let sum = ref(0)


    // 方法
    function add(){
        sum.value += 1
    }

    // 创建
    console.log('创建')

    // 挂载前
    onBeforeMount(()=>{
        console.log('挂载前')
    })

    // 挂载完毕
    onMounted(()=>{
        console.log('子----挂载完毕')
    })

    // 更新前
    onBeforeUpdate(()=>{
        console.log('更新前')
    })

    // 更新完毕
    onUpdated(()=>{
        console.log('更新完毕')
    })

    // 卸载前
    onBeforeUnmount(()=>{
        console.log('卸载前')
    })
    // 卸载完毕
    onUnmounted(()=>{
        console.log('卸载完毕')
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