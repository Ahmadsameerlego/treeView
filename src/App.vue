<template>
  <div>
  
  
    <vue-tree
      style="min-height:auto;    transform: translateY(179%);"
      :dataset="sampleData"
      :config="treeConfig"
      direction="horizontal"
      ref="tree"
      
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
  <div class="tree_interaction">
    <button @click="$refs.tree.zoomIn()">+</button>
    <button @click="$refs.tree.zoomOut()" style="margin:0 20px">-</button>
    <button @click="$refs.tree.restoreScale()"  >reset</button>
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
          {
            value: "2",
            children: [
              { value: "4" },
              {
                value: "5",
                children: [
                  {value : "I"},
                  {
                    value: "I I", children:[
                      {value: 1},
                      {value: 2},
                      {value: 3},
                  ]},
                ]
              },
              
            ]
          },
          { value: "3" , children : [ {value : "A"}, {value : "B"} ] },
          {
            value: "4",
            children: [
              { value: "IV" , children : [
               {value : "D"} ,
               {value : "C"} ,
               {value : "F"} ,
              ]},
              
            ]
          },
          {
            value: "5",
            children: [
              { value: "IV" , children : [
               {value : "D"} ,
               {value : "C"} ,
               {value : "F"} ,
              ]},
              
            ]
          }
        ],
      },
      treeConfig: { nodeWidth: 70, nodeHeight: 80, levelHeight: 200 },
    };
  },
  methods: {
   
    onClick() {
      this.showTree = true;
    },
  },
  mounted() {
    console.log(this.$refs.tree.treeChartCore.linkDataList.length);
    console.log(this.$refs.tree);
  }
};
</script>

<style>
.tree_interaction{
    position: fixed;
    top: 4%;
    right: 5%;
    background: #7592d5;
    padding: 12px;
    border-radius: 7px;

}
.tree-container{
  overflow: visible !important;
  height: auto;
  cursor: pointer;
}
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
