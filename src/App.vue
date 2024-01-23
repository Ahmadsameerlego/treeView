<template>
  <div>
  
  
    <vue-tree
      style="min-height:auto;    transform: translateY(179%);"
      :dataset="sampleData"
      :config="treeConfig"
      direction="horizontal"
      ref="tree"
      
    >
    <template v-slot:node="{ node, collapsed }" >
        <span
          class="tree-node"
          :style="{ border: collapsed ? '2px solid grey' : '' }"
          @click="getNode(collapsed)"
          >
          {{ node.value }}
          <div class="pop-up">
            data number {{  node.value }}
            {{  collapsed }}
          </div>
          </span
        >
        
      </template>
  </vue-tree>

  
  </div>
  <div class="tree_interaction">
    <button @click="$refs.tree.zoomIn()">+</button>
    <button @click="$refs.tree.zoomOut()" style="margin:0 20px">-</button>
    <button @click="$refs.tree.restoreScale()"  >reset</button>
  </div>

  <div class="tree_interaction tree_interaction2">
     <button @click="expand">
      toggle collapse
    </button>
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
    collapseNode(node) {
      node.collapsed = true;
    },
    getNode(status) {
      console.log(status)      
      this.$refs.tree.treeChartCore.nodeDataList[0]
    },
    // expandAllNodes(node, collapse = false) {
    //   node.collapsed = collapse;
    //   if (node.children) {
    //     node.children.forEach((child) => {
    //       this.expandAllNodes(child, collapse);
    //     });
    //   }
    // },
    expand() {
      document.querySelectorAll('.tree-node')[0].click()
    },

    


    onClick() {
      this.showTree = true;
    },
  },
  mounted() {
    console.log(this.$refs.tree.treeChartCore.nodeDataList[0].data._key);
    console.log(this.$refs.tree);
    

    setTimeout(() => {
      console.log()  
    }, 2000);
  }
};
</script>

<style>
.tree_interaction2{
      top: 16% !important;
}
.tree_interaction{
    position: fixed;
    top: 4%;
    right: 5%;
    background: #7592d5;
    padding: 12px;
    border-radius: 7px;
    width: 150px;
}
.tree-container{
  overflow: visible !important;
  height: auto;
  cursor: pointer;
}
.tree-node{
  position: relative;
  border-radius: 50%;
  background-color: #ccc;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  
}
.pop-up{
  position: absolute;
  min-width: fit-content;
  width:120px;
  height: 30px;
  background-color: #2c3e50;
  z-index: 11;
  color: #fff;
  border-radius: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
  left:55px;
  opacity: 0;
  transition: .3s all;
}
.tree-node:hover .pop-up{
  opacity: 1;
}
.pop-up::before{
    content: '';
    position: absolute;
    width: 20px;
    height: 20px;
    background-color: #2c3e50;
    left: -9px;
    transform: rotate(137deg);
    z-index: -1;
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
