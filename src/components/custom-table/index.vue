<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column
      v-for="column in newTableHeader"
      v-bind="column"
      v-html="'<span>This should be red.</span>'"
    ></el-table-column>
  </el-table>
  <!-- <div v-for="key in tableHeader">{{ key }}</div> -->
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
// TODO 在初次使用Mapper的章节中，值类型应该定义为string
export type Mapper<T> = {
  [P in keyof T as string]?: string | object;
};

const prop = defineProps<{
  // 注意，传入的参数都会toRaw作为prop的属性，只有prop是响应式的
  tableData: Array<any>;
  tableHeader: Mapper<any>;
}>();
const newTableHeader = ref({});
onMounted(() => {
  newTableHeader.value = { ...prop.tableHeader };
  const rawAttr = prop.tableHeader;
  for (let key in rawAttr) {
    let value = rawAttr[key];
    if (typeof value === "string") {
      Reflect.set(newTableHeader.value, key, {
        key: key,
        prop: key,
        label: value,
      });
    }

    if (typeof value === "object") {
      // 设置默认的key
      if (!Reflect.has(value, "key")) {
        Reflect.set(value, "key", key);
      }
      // 设置默认的prop
      if (!Reflect.has(value, "prop")) {
        Reflect.set(value, "prop", key);
      }
    }
  }
});
// const tableHeaders = computed(() => Object.keys(prop.tableData[0]));
</script>

<style scoped></style>
