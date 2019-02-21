<template>
  <div id="mountNode"></div>
</template>

<script>
  export default {
    name: 'BasicLayout',
    mounted () {
      this.initG6()
    }, data () {
      return {
        action: '',
        name: '',
        func: '',
        account: '',
        workflow: '',
        nodeType: 0,
        color: '',

        net: '',
        Util: '',
        workflowName: '',
        activation: '', //当前激活的节点
        isNode: false, //当前是节点
        isBlank: true,   //当前是空白区
        checked: true,  //网格对齐
        infoTitle: '画布',//属性标题
        oldColor: '',    //获取节点本身颜色
        type: '',        //有值为编辑状态
        datas: {
          nodes: [{
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

      registerShape () {
        G6.registerNode('customNode', {
          draw (item) {
            const group = item.getGraphicGroup()
            const model = item.getModel()
            group.addShape('text', {
              attrs: {
                x: 0,
                y: 0,
                fill: '#333',
                text: '我是一个自定义节点，\n有下面那个方形和我自己组成'
              }
            })
            group.addShape('text', {
              attrs: {
                x: 0,
                y: 0,
                fill: '#333',
                text: ' (' + model.x + ', ' + model.y + ') \n 原点是组的图坐标',
                textBaseline: 'top'
              }
            })
            group.addShape('circle', {
              attrs: {
                x: 0,
                y: 0,
                r: 4,
                fill: 'blue'
              }
            })
            return group.addShape('rect', {
              attrs: {
                x: 0,
                y: 0,
                width: 100,
                height: 100,
                stroke: 'red'
              }
            })
          }
        })

      },
      initG6 () {
        this.net = new G6.Net({
          container: 'mountNode',
          width: 500,
          height: 500,
          grid: {
            forceAlign: true, // 是否支持网格对齐
            cell: 30,         // 网格大小
            line: {           // 网格线样式
              stroke: '#ae3331'
            }
          }
        });

        this.net.read(this.datas);
      }
    }
  }
</script>

<style scoped>

</style>
