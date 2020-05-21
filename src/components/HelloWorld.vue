<template>
  <div>
    <h2>ref值：{{ city }}</h2>
    <h3>{{ Msg }}</h3>
    <h3>转换reactive类型数据{{ userInfo.userName }}</h3>
    <h3>转换reactive类型数据{{ code }}</h3>
    <button @click="increment">
      Count is: {{ state.count }}, double is: {{ state.double }}
    </button>
    <button @click="getCity">
      你来自哪里？
    </button>
    请输入年龄:<input type="text" v-model="age" /> <br /><br />
    我的年龄是:{{ userMsg }}
  </div>
</template>

<script>
import { ref, reactive, computed, isRef, toRefs } from 'vue'

export default {
  setup() {
    const city = ref('1')
    const Msg = ref('')
    const userName = ref('mrwholala')
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    })

    function increment() {
      state.count++
    }
    const getCity = () => {
      if (isRef(userName)) {
        Msg.value = `我叫：${userName.value},來自${city.value}`
      } else {
        Msg.value = `我叫：${userName.value}`
      }
    }
    const data = reactive({
      userInfo: {
        userName: 'xxxx'
      },
      code: 200
    })
    const age = ref('')
    //传入函数的方式
    const userMsg = computed(() => {
      return `我的年龄是:` + age.value
    })
    //传入对象自定义get set的形式
    //   const userMsg = computed({
    //   get(){
    //     return `computed-obj我的年龄是:`+age.value
    //   },
    //   set(val){
    //     age.value=val;
    //   }
    //  })

    console.log(data)
    console.log(toRefs(data))
    return {
      state,
      city,
      Msg,
      increment,
      getCity,
      ...toRefs(data),
      age,
      userMsg
    }
  }
}
</script>
