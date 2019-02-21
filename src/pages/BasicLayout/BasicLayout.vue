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
        grid:'',
        graph:'',

        data: {
          nodes: [{
            id: 'node1',
            x: 100,
            y: 200
          }, {
            id: 'node2',
            x: 300,
            y: 200
          }],
          edges:
            [{
              id: 'edge1',
              target: 'node2',
              source: 'node1'
            }]
        }
      }
    },
    methods: {
      initG6 () {
        this.grid = new G6.Plugins['tool.grid']();

        this.graph = new G6.Graph({
          container: 'mountNode',
          width: 500,
          height: 500,
          plugins: [this.grid]
        })
        this.graph.read(this.data)
        return graph
      }
    }
  }
</script>

<style scoped>

</style>
