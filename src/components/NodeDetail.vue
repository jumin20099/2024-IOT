<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

let nodeData = ref([]);

const getNodeData = (nodeId) => {
    axios.get('http://pcs.pah.kr:82/hardware/2C:F4:32:7B:C6:B1').then(response => {
      console.log(response.default);
      nodeData.value = response.data;
    }).catch(err => {
      console.error('노드 목록 조회 실패', err);
    })
}

onMounted(() => {
    getNodeData();
});
</script>

<template>
    <div>
        {{ nodeData }}
    </div>
</template>
