<template>
  <div id="mountNode"></div>
</template>

<script>
  import G6 from '@antv/g6'

  const data = {
    nodes: [{
      id: 'node1',
      x: 100,
      y: 200
    },{
      id: 'node2',
      x: 300,
      y: 200
    }],
    edges: [{
      id: 'edge1',
      target: 'node2',
      source: 'node1'
    }]
  };

  export default {
    name: 'BasicLayout',
    mounted () {
      this.initG6()
    }, methods: {
      initG6 () {
        const graph = new G6.Graph({
          container: 'mountNode',
          width: 500,
          height: 500
        });
        graph.read(data);
        return graph;
      }
    }
  }
</script>

<style scoped>

</style>
