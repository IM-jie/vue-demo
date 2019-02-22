<template>
  <div id="mountNode"></div>
</template>

<script>
  import G6 from '@antv/g6';
  import '@antv/g6/build/plugin.tool.grid';

  export default {
    name: 'BasicLayout',
    mounted () {
      this.initG6()
    },
    data () {
      return {
        grid:'',//网格
        graph:'',//绘图
        registerNode:'',//自定义新节点
        group:'',//group
        item:'',//数据模型

        data: {
          nodes: [{
            // shape: "customNode",
            id: 'node1',
            x: 100,
            y: 200
          }, {
            id: 'node2',
            x: 300,
            y: 100
          }, {
            id: 'node3',
            x: 300,
            y: 200
          }],

          edges: [{
            id: 'edge1',
            target: 'node2',
            source: 'node1'
          }, {
            id: 'edge2',
            target: 'node1',
            source: 'node2'
          }, {
            id: 'edge3',
            target: 'node1',
            source: 'node3'
          }]
        }
      }
    }, methods: {
      registerNewNode(){
        G6.registerNode('customNode', {
          draw(item){
            const group = item.getGraphicGroup();
            const model = item.getModel();
            group.addShape('text', {
              attrs: {
                x: 0,
                y: 0,
                fill: '#333',
                text: '我是一个自定义节点，\n有下面那个方形和我自己组成'
              }
            });
            group.addShape('text', {
              attrs: {
                x: 0,
                y: 0,
                fill: '#000000',
                text: ' ('+model.x+', '+model.y+') \n 原点是组的图坐标',
                textBaseline: 'top'
              }
            });
            group.addShape('circle', {
              attrs: {
                x: 0,
                y: 0,
                r: 1,
                fill: 'blue'
              }
            });
            return group.addShape('rect', {
              attrs: {
                x: 0,
                y: 0,
                width: 50,
                height: 50,
                stroke: '#000000'
              }
            });
          }
        });
      },

      initG6 () {
        // this.item = item.getModel();
        // this.group = this.graph.getGraphicGroup();
        // this.registerNewNode();
        this.grid = new G6.Plugins['tool.grid']();

        this.graph = new G6.Graph({
          container: 'mountNode',
          width: 500,
          height: 500,
          plugins: [this.grid]
        })
        this.graph.read(this.data);
        this.addAction();
      },
      addAction(){
        let node;
        let dx;
        let dy;
        this.graph.on('node:dragstart', ev=>{
          const {item} = ev;
          this.model = item.getModel();
          node = item;
          dx = this.model.x - ev.x;
          dy = this.model.y - ev.y;
        });
        this.graph.on('node:drag', ev=>{
          node && this.graph.update(node, {
            x: ev.x+dx,
            y: ev.y+dy
          });
        });
        this.graph.on('node:dragend', ev=>{
          node = undefined;
        });
      }
    }
  }
</script>

<style scoped>

</style>
