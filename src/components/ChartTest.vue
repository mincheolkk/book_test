<template>
  <div class="list-chart-div">
        <canvas  :id="result.detailData.isbn"/>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)

export default {
    props: ['madedData'],
    data(){
        return{
            
        }
    },

    methods: {
    makeData(timeData) {
     this.beforeChart = {
        "before":this.timeDivide(timeData["before"]),
        "after":this.timeDivide(timeData["after"]),
        "twoYear":this.timeDivide(timeData["twoYear"]),
        "fiveYear":this.timeDivide(timeData["fiveYear"]),       
        "sevenYear":this.timeDivide(timeData["sevenYear"])}     
        console.log(this.beforeChart);
        return this.beforeChart;
    },
    timeDivide(time) {
      if (time > 0) {
        return time
       } else if (time === undefined){
         return 0
       }
    },
    drawChart(timeData, isbn) {
      console.log("draw?")

     var chartData =  {
                labels:['a'],
                datasets:[
                    {
                        label:"before",
                        data:[timeData["before"]],
                        backgroundColor:"#4169e1"
                    },
                    {
                        label:"after",
                        data:[timeData["after"]],
                        backgroundColor:"#87ceeb"
                    },
                    {
                        label:'twoYear',
                        data:[timeData["twoYear"]],
                        backgroundColor:"#b0e0e6"
                    },
                    {
                        label:'fiveYear',
                        data:[timeData["fiveYear"]],
                        backgroundColor:"#b33e22"
                    },
                    {
                        label:'sevenYear',
                        data:[timeData["sevenYear"]],
                        backgroundColor:"#b82e12"
                    },
                ]
            };
    console.log(chartData)

    var ctx = document.getElementById(isbn)

     new Chart(ctx, {
        type: 'bar',
        data: chartData,
        options: this.options
      })
      console.log("end")
      // return newChart 
    }
  }

}
</script>

<style>

</style>