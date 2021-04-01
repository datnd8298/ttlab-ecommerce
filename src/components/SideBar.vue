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
              label: "T-Shirt",
              children: [],
            },
            {
              label: "Jean",
              children: [],
            },
            {
              label: "Jacket",
              children: [],
            },
            {
              label: "Vest",
              children: [],
            },
          ],
        },
        {
          label: "Women Clothing",
          children: [
            {
              label: "Level two 2-1",
              children: [
                {
                  label: "Level three 2-1-1",
                },
              ],
            },
            {
              label: "Level two 2-2",
              children: [
                {
                  label: "Level three 2-2-1",
                },
              ],
            },
          ],
        },
        {
          label: "Electronics",
          children: [
            {
              label: "Mobile Phone",
              children: [],
            },
            {
              label: "Laptop",
              children: [],
            },
            {
              label: "PC",
              children: [],
            },
            {
              label: "PC Gear",
              children: [
                {
                  label: "Screen",
                },
                {
                  label: "Keyboard",
                },
                {
                  label: "Mouse",
                },
                {
                  label: "VGA",
                },
                {
                  label: "Hard Drive",
                  children: [
                    {
                      label: "HDD",
                    },
                    {
                      label: "SSD",
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
              label: "Ring",
              children: [
                {
                  label: "Dimond",
                },
                {
                  label: "Platinum",
                },
                {
                  label: "Gold",
                },
                {
                  label: "Silver",
                },
              ],
            },
            {
              label: "Necklace",
              children: [
                {
                  label: "Dimond",
                },
                {
                  label: "Platinum",
                },
                {
                  label: "Gold",
                },
                {
                  label: "Silver",
                },
              ],
            },
            {
              label: "Bracelet",
              children: [
                {
                  label: "Dimond",
                },
                {
                  label: "Platinum",
                },
                {
                  label: "Gold",
                },
                {
                  label: "Silver",
                },
              ],
            },
            {
              label: "Earrings",
              children: [
                {
                  label: "Dimond",
                },
                {
                  label: "Platinum",
                },
                {
                  label: "Gold",
                },
                {
                  label: "Silver",
                },
              ],
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
      console.log(data);
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
