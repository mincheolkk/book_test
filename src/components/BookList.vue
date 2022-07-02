<template>
    <canvas id="myChart" width="400" height="400"></canvas>
    <h1> 개발자의 서재</h1>
    <div v-for="(result) in this.min" v-bind:key="result">
        <img :src="result.detailData.thumbnail" alt="image"/>
        <p>{{result.detailData.authors}}</p>
        <div>{{result.readTimeMap}}</div>
  </div>
  
</template>

<script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js">
import axios from "axios";

const ctx = document.getElementById('myChart').getContext('2d');
const myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: '# of Votes',
            data: [12, 19, 3, 5, 2, 3],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
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
});

export default {   
    mounted() {
        this.ttData();
  },

  data() {
    return {
      min:'',
      categories: ["June", "July", "Aug", "Sep", "Oct", "Nov", "Dec"],
  series: [
    {
      name: "Budget",
      data: [5000, 3000, 5000, 7000, 6000, 4000, 1000]
    },
    {
      name: "Income",
      data: [8000, 4000, 7000, 2000, 6000, 3000, 5000]
    },
    {
      name: "Expenses",
      data: [4000, 4000, 6000, 3000, 4000, 5000, 7000]
    },
    {
      name: "Debt",
      data: [3000, 4000, 3000, 1000, 2000, 4000, 3000]
    }
  ]
    }
  },

  methods: {
    ttData() {  
             axios
                .get('https://438d14e0-58fe-4eb2-8704-c2b65596f942.mock.pstmn.io/test')
                .then(res => {
                        console.log(res.data.resultList);
                        this.min = res.data.resultList;
                        for (var i=0; i<this.min.length; i++) {
                            console.log(this.min[0].readTimeMap)
                        }

                    })
                .catch(error => {
                        console.log(error)
                })
         }
  },

}
</script>

<style>

</style>