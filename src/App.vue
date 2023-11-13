<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column
      v-for="column in tableHeaders"
      :key="column"
      :prop="column"
      :label="column + 'Name'"
      width="180"
    ></el-table-column>
  </el-table>
</template>

<script lang="ts" setup>
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
