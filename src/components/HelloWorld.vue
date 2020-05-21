<template>
  <h2>ref值：{{ city }}</h2>
  <button @click="increment">
    Count is: {{ state.count }}, double is: {{ state.double }}
  </button>
  <button @click="getCity">
    你来自哪里？
  </button>
</template>

<script>
import { ref, reactive, computed } from "vue";

export default {
  setup() {
    const city = ref("1");
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    });

    function increment() {
      state.count++;
    }
    const getCity = () => {
      city.value = "cd";
    };

    return {
      state,
      city,
      increment,
      getCity
    };
  }
};
</script>
