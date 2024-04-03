<script setup lang="ts">


const charts = ["饼图", "直方图", "力导向图"];
function navigateChart(){

}
</script>

<template>
  <div class="aside">
    <div class="chart" v-for="chart in charts" :key="chart" @click="navigateChart">
      {{ chart }}
    </div>
  </div>
</template>

<style scoped>
.aside {
  position: fixed;
  left: 50px;
  top: 50%;
  margin-top: -20vh;
  width: 12vw;
  height: 40vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border-left: 2px solid;
  border-right: 2px solid;
  /*设置线性渐变*/
  border-image: linear-gradient(
      180deg,
      rgba(255, 255, 255, 0) 0%,
      #104b8d 20%,
      rgba(255, 255, 255, 0) 99%
    )
    2 2 2 2;
}
.chart{
    height:5vh;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 12vw;
}
.chart:hover{
    background-color: #0a287b;
}
</style>
