<script setup>
import HelloWorld from "./HelloWorld.vue";
import { ref } from "vue";
import axios from "axios";
import { onMounted } from "vue"

let count = ref(0);
let nodeList = ref([
    { mac_address: "48:3F:DA:0C:B2:FU", name: "node-heoshin" },
    { mac_address: "14:ED:C9:75:54:CK", name: null },
]);

const getNodeList = () =>{
  axios.get('http://pcs.pah.kr:82/hardware').then(response => {
      console.log(response.default);
      nodeList.value = response.data;
    }).catch(err => {
      console.error('노드 목록 조회 실패', err);
    })
}

getNodeList();
</script>

<template>
  <h2>노드 목록</h2>
  <p>노드 개수 : {{ nodeList.length }}</p>

  <div v-for="(item, idx) in nodeList">
    <button>{{ nodeList[idx]["mac_address"] }}</button>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
