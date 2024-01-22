<template>
  <div>
<diV>
    <h1>Code Base</h1>
  </diV>
    <vue-tree
      style="min-height:150vh"
      :dataset="sampleData"
      :config="treeConfig"
      direction="horizontal"
    >
    <template v-slot:node="{ node, collapsed }">
        <span
          class="tree-node"
          :style="{ border: collapsed ? '2px solid grey' : '' }"
          >{{ node.value }}</span
        >
      </template>
  </vue-tree>

  
  </div>
</template>

<script>
import VueTree from "./vue-tree/VueTree.vue";

export default {
  components: { VueTree },
  data() {
    return {
      showTree: false,
      sampleData: {
        value: "1",
        children: [
          { value: "2", children: [{ value: "4" }, { value: "5" }] },
          { value: "3" , children : [ {value : "A"}, {value : "B"} ] },
          {value : "4" ,  children : [ {value : "IV"} ]}
        ],
      },
      treeConfig: { nodeWidth: 120, nodeHeight: 80, levelHeight: 200 },
    };
  },
  methods: {
   
    onClick() {
      this.showTree = true;
    },
  },
};
</script>

<style>
.tree-node{
  border-radius: 50%;
  background-color: #ccc;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
