<template>
  <canvas ref="chart" :width="width" :height="height"></canvas>
</template>

<script>
import Chart from 'chart.js'

export default {
  name: 'vue-chart',

  props: {
    type: {
      required: true,
      type: String
    },
    data: {
      required: true,
      type: [Object, Array]
    },
    options: Object,
    width: Number,
    height: Number
  },

  data: () => ({
    chart: ''
  }),

  watch: {
    'data.labels' () {
      this.chart.update()
    },

    'data.datasets' () {
      this.chart.update()
    }
  },

  methods: {
    createChart () {
      this.chart = new Chart(this.$refs.chart, {
        type: this.type,
        data: this.data,
        options: this.options
      })
    }
  },

  mounted () {
    this.createChart()
  },

  beforeDestroy () {
    this.chart.destroy()
  }
}
</script>
