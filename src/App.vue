<template>
  <CustomTable
    :table-data="tableData"
    :table-headers="tableHeaders"
  ></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
const tableData = new Array(9).fill({
  a: "2016-05-03",
  b: "Tom",
  c: "No. 189, Grove St, Los Angeles",
  d: "No. 189, Grove St, Los Angeles",
  e: "2016-05-03",
  f: "Tom",
  g: "No. 189, Grove St, Los Angeles",
  h: "2016-05-03",
  i: "Tom",
});
const tableHeaders = Object.keys(tableData[0]);
</script>
