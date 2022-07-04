<template>
    <h1> 개발자의 서재</h1>
    <div v-for="(result) in this.min" v-bind:key="result" class="shadow">
        <img :src="result.detailData.thumbnail" alt="image"/>
        <p>{{result.detailData.authors}}</p>
        <p>{{result}}</p>
        <div>{{result.readTimeMap}}</div>
        <div>
            <canvas ref="barChart"/>
        </div>

    </div>
    
    
  
</template>

<script>
import axios from "axios";
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)

let caseChart;

export default {   
 
  async mounted(){
    this.$nextTick(function () {
      this.ttData();
      this.createChart()
    })
  },


  data() {
    return {
      min:'',

      data:  {
                labels:['a'],
                datasets:[
                    {
                        label:"ks",
                        data:[42],
                        backgroundColor:"#4169e1"
                    },
                    {
                        label:"m",
                        data:[48],
                        backgroundColor:"#87ceeb"
                    },
                    {
                        label:'c',
                        data:[39],
                        backgroundColor:"#b0e0e6"
                    },
                    {
                        label:'d',
                        data:[1],
                        backgroundColor:"#b33e22"
                    }
                ]
            
            },
    options: {
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
    }
    
    }
  },
  

    methods: {
   async ttData() {  
             await axios
                .get('https://438d14e0-58fe-4eb2-8704-c2b65596f942.mock.pstmn.io/test')
                .then(res => {
                        console.log(res.data.resultList);
                        this.min = res.data.resultList;
                    })
                .catch(error => {
                        console.log(error)
                })
         },

    createChart() {
        console.log(caseChart);
        if (caseChart !== undefined){
            caseChart.destroy();
        }

      caseChart = new Chart(this.$refs.barChart, {
        type: 'bar',
        data: this.data,
        options: this.options
      })
      console.log(caseChart);
    },

    }
  
    


}
</script>

<style>
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>

