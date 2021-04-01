<template>
  <div>
    <div class="logo">
      <el-row>
        <el-col :span="4">
          <img
            src="@/assets/Letter.png"
            alt=""
            style="width: 40px; height: 40px; background-color: blue"
          />
          <img src="@/assets/Name.png" alt="" />
        </el-col>
        <el-col :span="8">
          <el-input
            placeholder="Search"
            prefix-icon="el-icon-search"
            v-model="searchString"
            @keyup="liveSearch"
          />
        </el-col>
      </el-row>
    </div>
    <div class="category-list">
      <!-- <Category @click="selectedCate" :categories="getCategoryList" /> -->
    </div>
    <div class="filter">
      <el-row>
        <el-col :span="18">
          <el-tag><i class="el-icon-s-operation" />Bộ lọc</el-tag>
          <el-select
            v-model="filtedPrice"
            placeholder="Lọc theo giá"
            @change="filterProduct"
          >
            <el-option
              v-for="item in prices"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-col>
      </el-row>
    </div>
    <div class="product">
      <el-row>
        <el-col :span="6"><SideBar /></el-col>
        <el-col :span="18">
          <ProductList :products="getProductList" />
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
// import Category from "./Category";
import SideBar from "./SideBar";
import ProductList from "./ProductList";
import axios from "axios";
// import _ from "lodash";

export default {
  components: {
    // Category,
    SideBar,
    ProductList,
  },

  data() {
    return {
      productList: [],
      categories: ["men clothing", "women clothing", "electronics", "jewelery"],
      filtedProducts: [],
      filtedPrice: "",
      filtedCate: "",
      searchString: "",
      prices: [
        {
          label: "< $50.0",
          value: 50,
        },
        {
          label: "$50.0 - $100.0",
          value: 100,
        },
        {
          label: "$100.0 - $500.0",
          value: 500,
        },
        {
          label: "$500.0 - $750.0",
          value: 750,
        },
        {
          label: "$750.0 - $1000.0",
          value: 1000,
        },
        {
          label: "> $1000.0",
          value: 1001,
        },
      ],
    };
  },

  computed: {
    getProductList() {
      return this.filtedProducts ? this.filtedProducts : [];
    },

    getCategoryList() {
      return this.categories ? this.categories : [];
    },
  },

  methods: {
    getAllProduct() {
      axios("https://fakestoreapi.com/products")
        .then((res) => {
          this.parseData(res.data);
        })
        .catch((err) => err);
    },

    parseData(data) {
      this.productList = data;
      this.filtedProducts = data;
    },

    filterProduct() {
      this.filtedProducts = this.productList.filter(this.fillPro);
      console.log(this.filtedProducts);
    },

    fillPro(product) {
      if (this.filtedCate != null) {
        if (product.category === this.filtedCate) {
          switch (this.filtedPrice) {
            case 0:
              return product;

            case 50:
              if (product.price < 50) {
                return product;
              }
              break;

            case 100:
              if (50 < product.price < 100) {
                return product;
              }
              break;

            case 500:
              if (100 < product.price < 500) {
                return product;
              }
              break;

            case 750:
              if (500 < product.price < 750) {
                return product;
              }
              break;

            case 1000:
              if (750 < product.price < 1000) {
                return product;
              }
              break;

            case 1001:
              if (1000 < product.price) {
                return product;
              }
              break;
          }
        }
      } else {
        switch (this.filtedPrice) {
          case 0:
            return product;

          case 50:
            if (product.price < 50) {
              return product;
            }
            break;

          case 100:
            if (50 < product.price < 100) {
              return product;
            }
            break;

          case 500:
            if (100 < product.price < 500) {
              return product;
            }
            break;

          case 750:
            if (500 < product.price < 750) {
              return product;
            }
            break;

          case 1000:
            if (750 < product.price < 1000) {
              return product;
            }
            break;

          case 1001:
            if (1000 < product.price) {
              return product;
            }
            break;
        }
      }
      // return product;
    },

    liveSearch() {
      this.filtedProducts = this.productList.filter((product) => {
        if (product.title.includes(this.searchString) == true) {
          return product;
        }
      });
      console.log(this.filtedProducts);
    },
  },

  created() {
    this.getAllProduct();
  },
};
</script>

<style></style>
