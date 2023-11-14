<template>
  <CustomTable :table-data="tableData" v-loading="loading">
    <CustomColumn :table-header="tableHeaderMapper">
      aaa
      <!-- 需要解构使用 -->
      <template #default-b="scope"> hello{{ scope.$index }} </template>
      <template #header-a>word</template>
    </CustomColumn>
    <!-- hhh -->
    <template #empty>自定义空状态</template>
    <!-- <template #append> 空 </template> -->
  </CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import CustomColumn from "./components/custom-column/index.vue";
// import CustomButton from "./components/custom-button/index.vue";
import { onMounted, ref } from "vue";
import { getData } from "./api/index";
const tableData = ref([]);
// 定义新的Header结构，key为column的prop/key，value为column的name
const tableHeaderMapper = {
  a: {
    label: "列a",
    // slotName: "aaa",
  },
  b: {
    label: "bb",
    // slotName: "bb",
  },
  c: "列c",
  d: "列d",
  e: "列e",
  f: "列f",
  g: "列g",
  h: "列h",
  i: "列i",
};
const loading = ref(false);
onMounted(() => {
  loading.value = true;
  getData().then((res: any) => {
    tableData.value = res.data;
    loading.value = false;
  });
});
</script>
