<template>
  <el-table :data="tableData" style="width: 100%">
    <template v-for="slot in Object.keys(slots)" #[slot]>
      <slot :name="slot"></slot>
    </template>
  </el-table>
  <!-- <component :is="slotsComp[0]"></component> -->
</template>

<script setup lang="ts">
// import { onMounted, useSlots, ref, h } from "vue";
import { onMounted, useSlots } from "vue";

defineProps<{
  tableData: Array<any>;
}>();
const slots = useSlots();

onMounted(() => {
  // const keys = Object.keys(slots);
  // console.log(Object.keys(slots));
  // slotsComp.value = [];
  // for (let key of keys) {
  //   slotsComp.value.push(h("div", slots[key]()));
  //   // console.log(slots[key]);
  // }
  // // slotsComp.value[0] = h("div", );
  // console.log(slotsComp);
});
</script>

<style scoped></style>
