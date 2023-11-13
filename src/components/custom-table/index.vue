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
import { computed } from "vue";

const prop = defineProps<{
  // 注意，传入的参数都会toRaw作为prop的属性，只有prop是响应式的
  tableData: Array<any>;
}>();
const tableHeaders = computed(() => Object.keys(prop.tableData[0]));
</script>

<style scoped></style>
