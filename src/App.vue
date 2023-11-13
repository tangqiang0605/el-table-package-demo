<template>
  <CustomTable
    :table-data="tableData"
    :table-header="tableHeaderMapper"
    v-loading="loading"
  ></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import CustomButton from "./components/custom-button/index.vue";
import { onMounted, ref, h } from "vue";
import { getData } from "./api/index";
const tableData = ref([]);
// 定义新的Header结构，key为column的prop/key，value为column的name
const tableHeaderMapper = {
  a: {
    label: "列a",
    width: "400px",
    // component: CustomButton,
    inner: h("div", { class: "bar", innerHTML: "hello" }),
    // inner: "<div>hellohtml</div>",
  },
  b: "列b",
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
