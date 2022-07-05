<template>
  <div id="app">
    <BookList
      v-bind:propsdata="min"
      v-on:testTime="makeData"
      v-on:makeChart="drawChart"
      >BookList</BookList>
    <TestChart :height="'50px'" :first-data="20" :second-data="'80'"/>
    
  </div>
</template>

<script>
import BookList from './components/BookList.vue'
import TestChart from './components/TestChart.vue'
import axios from "axios";
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)

// let newChart;

export default {
  name: 'App',

  components: {
    BookList,
    TestChart
  },
  data() {
    return {
      min: '',
      timeData:'',
      isbn:'',
      beforeChart:[],
      // newChart:'',
      options:{
          scales: {
              x:{
                  stacked:true,
                  display:false
              },
              y: {
                  stacked:true,
                  display:false
              }
          },
          indexAxis:'y',
          plugins:{
              legend:{
                  display:true
              }
          }
      },
    }
  },
   
//   async mounted(){
//     this.$nextTick(function () {
//       this.createChart()
//     })
//   },


  created() {
     this.min = axios
                .get('https://438d14e0-58fe-4eb2-8704-c2b65596f942.mock.pstmn.io/test')
                .then(res => {

                        this.min = res.data.resultList;
                    })
                .catch(error => {
                        console.log(error)
                })
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
      // if (newChart !== undefined) {
      //   console.log("destory? ")
      //   newChart.destroy();
      //   console.log("destory !")
      // }
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
