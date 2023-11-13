<template>
  <!-- <el-table :data="tableData" style="width: 100%">
    <el-table-column
      v-for="column in tableHeader"
      :key="column"
      :prop="column"
      :label="column + 'Name'"
      width="180"
    ></el-table-column>
  </el-table> -->
  <div v-for="key in tableHeader">{{ key }}</div>
</template>

<script setup lang="ts">
export type Mapper<T> = {
  [P in keyof T as string]?: string | object;
};

defineProps<{
  // 注意，传入的参数都会toRaw作为prop的属性，只有prop是响应式的
  tableData: Array<any>;
  tableHeader: Array<Mapper<any>>;
}>();

// const tableHeaders = computed(() => Object.keys(prop.tableData[0]));
</script>

<style scoped></style>
