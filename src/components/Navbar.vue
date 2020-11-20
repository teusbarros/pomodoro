<template>
  <div id="nav">
    <img src="../../public/pomodoro.png" alt="Pomodoro" v-if="workTime">
    <img src="../../public/pomodoro1.png" alt="Pomodoro" v-else>
  </div>
</template>
<script>
export default {
  props:{
    workTime: Boolean
  }
};
</script>
<style scoped>
img{
    height: 65px;
    margin-top: 10px;
}
#nav{
  margin-bottom: 3%;
  padding: 2%;
}
</style>