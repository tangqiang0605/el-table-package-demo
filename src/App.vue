<template>
  <CustomTable
    :table-data="tableData"
    :table-header="tableHeaderMapper"
  ></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import { onMounted, ref } from "vue";
import { getData } from "./api/index";
const tableData = ref([]);
// 定义新的Header结构，key为column的prop/key，value为column的name
const tableHeaderMapper = {
  a: "列a",
  b: "列b",
  c: "列c",
  d: "列d",
  e: "列e",
  f: "列f",
  g: "列g",
  h: "列h",
  i: "列i",
};
onMounted(() => {
  getData().then((res: any) => {
    tableData.value = res.data;
  });
});
</script>
