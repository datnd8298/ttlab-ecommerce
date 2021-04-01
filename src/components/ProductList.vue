<template>
  <div>
    <el-row>
      <el-col :span="6" v-for="(product, index) in getProducts" :key="index">
        <el-card :body-style="{ padding: '0px', height: '400px' }">
          <img
            :src="product.image"
            class="image"
            style="width: 200px; height: 200px"
          />
          <div style="padding: 14px">
            <p>{{ product.title }}</p>
            <div class="bottom clearfix">
              <p>${{ product.price }}</p>
              <el-button type="text" class="button">Add to cart</el-button>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  props: {
    products: Array,
  },

  computed: {
    getProducts() {
      return this.products ? this.products : "none";
    },
  },
};
</script>

<style></style>
