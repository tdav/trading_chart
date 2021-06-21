<template>
  <div class="hello">
    <TradingVue
      title-txt="Chart"
      :toolbar="true"
      :data="chartData"      
    />
  </div>
</template>

<script>

import { TradingVue , DataCube} from "trading-vue-js";
import axios from "axios";

export default {
  name: "Chart",
components: { TradingVue },
  beforeCreate() {
    axios
      .get("/data.json")
      .then((response) => 
        {
        this.chartData = new DataCube(response.data)
        });
  },

  data() {
    return {
      chartData: {},
    };
  },
};
</script>