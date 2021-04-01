<template>
  <el-row
    ><el-button v-for="(cate, index) in categories" :key="index" round>{{
      cate
    }}</el-button></el-row
  >
</template>

<script>
export default {
  props: {
    categories: Array,
  },
};
</script>

<style scoped>
el-row {
  display: flex;
  justify-content: left;
}
</style>
