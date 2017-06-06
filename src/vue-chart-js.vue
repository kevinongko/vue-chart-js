<template>
  <canvas ref="chart" :width="width" :height="height"></canvas>
</template>

<script>
import Chart from 'chart.js'

export default {
  name: 'chart',

  props: {
    type: {
      required: true,
      type: String
    },
    data: {
      required: true,
      type: Object
    },
    options: Object,
    width: Number,
    height: Number
  },

  data: () => ({
    chart: ''
  }),

  watch: {
    'data' () {
      this.chart.destroy()
      this.$nextTick(() => {
        this.createChart()
      })
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
