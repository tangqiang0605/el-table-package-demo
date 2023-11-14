<template>
  <el-table-column v-for="column in newTableHeader" v-bind="column">
    <template #default="scope">
      <div v-if="column.inner">
        <div v-if="typeof column.inner == 'string'" v-html="column.inner"></div>
        <component v-else :is="column.inner"></component>
      </div>
      <div v-if="column.slotName">
        <slot :name="column.slotName" :item="scope.row"></slot>
      </div>
    </template>
    <template #column></template>
    <!-- 外部分割定义，插槽-列 -->
    <!-- <template v-for="slot in Object.keys(slots || {})" #[slot]>
      <slot :name="slot"></slot>
    </template> -->
  </el-table-column>
  <!-- </div> -->
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUpdate, markRaw, useSlots } from "vue";
// TODO 在初次使用Mapper的章节中，值类型应该定义为string
export type Mapper<T> = {
  [P in keyof T as string]?: string | object;
};
import { valueEquals } from "element-plus";

const prop = defineProps<{
  // 注意，传入的参数都会toRaw作为prop的属性，只有prop是响应式的
  // tableData: Array<any>;
  tableHeader: Mapper<any>;
}>();
// defineSlots<{
//   default(): any;
// }>();
const slot = useSlots();
const newTableHeader = ref<any>({});
const genNewTableHeader = () => {
  newTableHeader.value = { ...prop.tableHeader };
  const rawAttr = prop.tableHeader;
  for (let key in rawAttr) {
    let column = rawAttr[key];
    if (typeof column === "string") {
      Reflect.set(newTableHeader.value, key, {
        key: key,
        prop: key,
        label: column,
      });
    }

    if (typeof column === "object") {
      // 设置默认的key
      if (!Reflect.has(column, "key")) {
        Reflect.set(column, "key", key);
      }
      if (!Reflect.has(column, "label")) {
        Reflect.set(column, "label", key);
      }
      // 设置默认的prop
      if (
        !Reflect.has(column, "prop") &&
        !(
          Reflect.has(column, "type") &&
          Reflect.get(column, "type") == "selection"
        )
      ) {
        Reflect.set(column, "prop", key);
      }
      if (Reflect.has(column, "component")) {
        Reflect.set(
          column,
          "component",
          markRaw(Reflect.get(column, "component"))
        );
      }
      if (Reflect.has(column, "slotName")) {
        if (Reflect.has(slot, column.slotName)) {
        } else {
          console.warn("custom-column：您定义了slotName却没有使用");
          Reflect.set(column, "slotName", undefined);
        }
      }
    }
  }
};
onMounted(genNewTableHeader);
onBeforeUpdate(genNewTableHeader);
</script>

<style scoped></style>
