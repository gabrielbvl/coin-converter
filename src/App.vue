<template>
  <div class="container grid-lg my-2 py-2 text-dark">
    <div class="card">
      <div class="cardHeader">
        <div class="h4">Moedas</div>
      </div>
      <div class="cardBody">
        <CoinData :quotes="quotes" />
      </div>
    </div>
  </div>
</template>

<script>
import CoinData from "./components/CoinData.vue";
import api from "@/server/api.js";
import { onMounted, reactive, toRefs } from "vue";

export default {
  name: "App",
  components: {
    CoinData,
  },

  setup() {
    const data = reactive({
      quotes: {},
    });

    onMounted(async () => {
      const response = await api.all();
      data.quotes = response.data;
    });
    return { ...toRefs(data) };
  },
};
</script>

<style>
.h4 {
  text-align: center;
  margin-bottom: 10px;
}

.card {
  box-shadow: inset 0 0 1em gold, 0 0 2em silver;
  padding: 10px;
}
</style>
