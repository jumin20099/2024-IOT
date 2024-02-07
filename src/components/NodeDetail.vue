<script setup>
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';
import VueApexCharts from 'vue3-apexcharts'

let nodeData = ref([]);

const props = defineProps({
  currentNodeId: String,
})

let foundValue = null;

watch(() => props.currentNodeId, (newVal, oldVal) => {
  console.log("props.currentNodeId 변경됨.", newVal)
  getNodeData(newVal);
})

const getNodeData = (currentNodeId) => {
    axios.get('http://pcs.pah.kr:82/hardware/' + currentNodeId["mac_address"]).then(response => {
      console.log(response.default);
      nodeData.value = response.data;
      chartSeriesfoundValue.value[0].data = [];
      for (i of nodeData) {
        console.log(i)
        if (i['temperature'] == 22.3) {
          foundValue = i['']
        }
        return foundValue;
      }
    }).catch(err => {
      console.error('노드 목록 조회 실패', err);
    })
}

const chartOptions = ref({

})

const chartSeries = ref([
  {
  name : 'Temperature',
  data : [],
  }
])
</script>
<template>
    <div>
        <h2>노드 데이터</h2>
        <p>Node Id : {{ props.currentNodeId["mac_address"]}}</p>
        <VueApexCharts width="100%" type="line" :options="chartOptions" :series="chartSeries"></VueApexCharts>
        <div class="nodeDataDiv">{{ nodeData }}</div>
    </div>
</template>

<style scoped>
.nodeDataDiv{
  max-width: 300px;
}
</style>