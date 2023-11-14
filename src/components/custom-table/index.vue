<template>
  <el-table :data="tableData" style="width: 100%">
    <template v-for="slot in Object.keys(slots)" #[slot]>
      <slot :name="slot"></slot>
    </template>
  </el-table>
</template>

<script setup lang="ts">
import { useSlots } from "vue";

defineProps<{
  tableData: Array<any>;
}>();
const slots = useSlots();
</script>

<style scoped></style>
