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

<script setup lang="ts">
defineProps({
  tableData: Array<any>,
  tableHeaders: Array<any>,
});
</script>

<style scoped></style>
