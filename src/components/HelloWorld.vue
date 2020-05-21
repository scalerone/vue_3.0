<template>
  <div>
    <h2>ref值：{{ city }}</h2>
    <h3>{{Msg}}</h3>
    <button @click="increment">
      Count is: {{ state.count }}, double is: {{ state.double }}
    </button>
    <button @click="getCity">
      你来自哪里？
    </button>
  </div>
</template>

<script>
import { ref, reactive, computed, isRef } from "vue";

export default {
  setup() {
    const city = ref("1");
    const Msg = ref("");
    const userName = ref("mrwholala");
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    });

    function increment() {
      state.count++;
    }
    const getCity = () => {
      if (isRef(userName)) {
        Msg.value = `我叫：${userName.value},來自${city.value}`;
      } else {
        Msg.value = `我叫：${userName.value}`;
      }
    };

    return {
      state,
      city,
      Msg,
      increment,
      getCity
    };
  },
};
</script>
