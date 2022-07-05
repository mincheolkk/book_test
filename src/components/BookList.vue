<template>
    <h1> 개발자의 서재</h1>
    <div v-for="(result) in propsdata" v-bind:key="result" class="shadow">
        <img :src="result.detailData.thumbnail" alt="image"/>
        <p>{{result.detailData.authors}}</p>
        <button v-on:click="pleaseTime(result)">button</button>
        <button v-on:click="pleaseChart(result)">chart</button>
        <div>{{result.readTimeMap}}</div>
        
        <canvas :id="result.detailData.isbn"/>
    </div>
  
</template>

<script>

export default {   
 
//   async mounted(){
//     this.$nextTick(function () {
//       this.createChart()
//     })
//   },



  data() {
    return {
    }
  },
  props: ['propsdata'],

    methods: {
        pleaseTime(result) {
            this.$emit('testTime',result.readTimeMap)
        },
        pleaseChart(result) {
            this.$emit('makeChart',result.readTimeMap, result.detailData.isbn)
        },
    }
}
</script>

<style>
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>

