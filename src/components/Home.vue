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
          <el-select v-model="filtedPrice" placeholder="Lọc theo giá">
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
        <el-col :span="6"
          ><SideBar @selectedCate="filterCate($event)"
        /></el-col>
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
      filtedCate: {
        cate: "",
        label: "",
      },
      searchString: "",
      prices: [
        {
          label: "All",
          value: 0,
        },
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
      this.filterProduct();
      return this.filtedProducts;
    },

    getCategoryList() {
      return this.categories ? this.categories : [];
    },
  },

  methods: {
    async getAllProduct() {
      await axios("https://fakestoreapi.com/products")
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
      this.filtedProducts = this.productList.filter((product) => {
        if (this.filtedCate.cate != "") {
          if (product.category === this.filtedCate.cate) {
            if (
              this.filtedCate.label != "" &&
              product.title.includes(this.filtedCate.label) == true
            ) {
              if (this.searchString != "") {
                console.log(this.searchString);
                if (product.title.includes(this.searchString) == true) {
                  return this.filterPrice(product);
                }
              } else {
                return this.filterPrice(product);
              }
            }
          }
        } else {
          if (this.searchString != "") {
            console.log(this.searchString);
            if (product.title.includes(this.searchString) == true) {
              return this.filterPrice(product);
            }
          } else {
            return this.filterPrice(product);
          }
        }
      });
    },

    filterCate(data) {
      if (data.children.length == 0) {
        this.filtedCate.cate = data.value;
        this.filtedCate.label = data.label;
      }
    },

    filterPrice(product) {
      if (this.filtedPrice != "") {
        switch (this.filtedPrice) {
          case 0:
            return product;

          case 50:
            if (product.price < 50) {
              return product;
            }
            break;

          case 100:
            if (50 < product.price && product.price < 100) {
              return product;
            }
            break;

          case 500:
            if (100 < product.price && product.price < 500) {
              return product;
            }
            break;

          case 750:
            if (500 < product.price && product.price < 750) {
              return product;
            }
            break;

          case 1000:
            if (750 < product.price && product.price < 1000) {
              return product;
            }
            break;

          case 1001:
            if (1000 < product.price) {
              return product;
            }
            break;
        }
      } else {
        return product;
      }
    },

    liveSearch() {
      console.log(this.searchString);
      // this.filtedProducts = this.productList.filter((product) => {
      //   if (product.title.includes(this.searchString) == true) {
      //     return product;
      //   }
      // });
    },
  },

  created() {
    this.getAllProduct();
  },
};
</script>

<style></style>
