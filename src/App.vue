<template>
  <CustomTable
    :table-data="tableData"
    :table-header="tableHeaderMapper"
  ></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import { ref } from "vue";
const tableData = ref(
  new Array(9).fill({
    a: "2016-05-03",
    b: "Tom",
    c: "No. 189, Grove St, Los Angeles",
    d: "No. 189, Grove St, Los Angeles",
    e: "2016-05-03",
    f: "Tom",
    g: "No. 189, Grove St, Los Angeles",
    h: "2016-05-03",
    i: "Tom",
  })
);
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
</script>
