<template>
  <div>
    <canvas
      ref="barChart"
      :height="height"
    />
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)
let chart 
export default {
  props:{
    height:{
      type:String,
      required:true
    },
    firstData:{


    },
    secondData:{
      type:String,
      required:true
    }
  },
  data:() => ({
    chartData: {
      labels: [ 'firstData', 'secondData' ],
      datasets: [{
        data:[],
        backgroundColor: [
          'rgba(255, 99, 132, 0.2)',
          'rgba(54, 162, 235, 0.2)',
        ],
        borderColor: [
          'rgba(255, 99, 132, 1)',
          'rgba(54, 162, 235, 1)',
        ],
        borderWidth: 1
      }]
    },
    options: {
      scales: {
        y: {
          beginAtZero: true
        }
      }
    }
  }),
  watch:{
    firstData(){
      this.createChart()
    },
    secondData(){
      this.createChart()
    },
    deep: true
  },
  async mounted(){
    this.$nextTick(function () {
      this.createChart()
    })
  },
  methods:{
    createChart(){
      if (chart !== undefined){
        chart.destroy()
      }
      chart =  new Chart(this.$refs.barChart, {
        type:'bar',
        data:this.chartData,
        options:this.options
      })
      chart.data.datasets[0].data[0] = this.firstData
      chart.data.datasets[0].data[1] = this.secondData
      chart.update()
    },
  },
}
</script>