<template>
  <div>
    <div class="headTitle">
      <h1>Departments</h1>
    </div>
    <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          label: "Men Clothing",
          children: [
            {
              value: "men clothing",
              label: "T-Shirt",
              children: [],
            },
            {
              value: "men clothing",
              label: "Jean",
              children: [],
            },
            {
              value: "men clothing",
              label: "Jacket",
              children: [],
            },
            {
              value: "men clothing",
              label: "Vest",
              children: [],
            },
          ],
        },
        {
          label: "Women Clothing",
          children: [
            {
              value: "women clothing",
              label: "T-Shirt",
              children: [],
            },
            {
              value: "women clothing",
              label: "Jean",
              children: [],
            },
            {
              value: "women clothing",
              label: "Jacket",
              children: [],
            },
            {
              value: "women clothing",
              label: "Vest",
              children: [],
            },
          ],
        },
        {
          label: "Electronics",
          children: [
            {
              value: "electronics",
              label: "Mobile Phone",
              children: [],
            },
            {
              value: "electronics",
              label: "Laptop",
              children: [],
            },
            {
              value: "electronics",
              label: "PC",
              children: [],
            },
            {
              value: "electronics",
              label: "PC Gear",
              children: [
                {
                  value: "electronics",
                  label: "Screen",
                  children: [],
                },
                {
                  value: "electronics",
                  label: "Keyboard",
                  children: [],
                },
                {
                  value: "electronics",
                  label: "Mouse",
                  children: [],
                },
                {
                  value: "electronics",
                  label: "VGA",
                  children: [],
                },
                {
                  value: "electronics",
                  label: "Hard Drive",
                  children: [
                    {
                      value: "electronics",
                      label: "HDD",
                      children: [],
                    },
                    {
                      value: "electronics",
                      label: "SSD",
                      children: [],
                    },
                  ],
                },
              ],
            },
          ],
        },
        {
          label: "Jewelery",
          children: [
            {
              value: "jewelery",
              label: "Dimond",
              children: [],
            },
            {
              value: "jewelery",
              label: "Platinum",
              children: [],
            },
            {
              value: "jewelery",
              label: "Gold",
              children: [],
            },
            {
              value: "jewelery",
              label: "Silver",
              children: [],
            },
          ],
        },
      ],
      defaultProps: {
        children: "children",
        label: "label",
      },
    };
  },
  methods: {
    handleNodeClick(data) {
      this.$emit("selectedCate", data);
    },
  },
};
</script>

<style scoped>
.headTitle h1 {
  border: 2px;
  border-style: solid;
  border-radius: 30px;
}
</style>
