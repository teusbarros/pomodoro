<template>
  <div class="container">
    <div class="progress" >
      <div
        class="progress-bar"
        :class="bgCor"
        role="progressbar"
        :aria-valuenow="{ percentual }"
        aria-valuemin="0"
        aria-valuemax="100"
        :style="{ width: percentual + '%' }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    workTime: Boolean,
    percentual: Number
  },
  computed:{    
    bgCor:function () {
        return this.workTime ? "bar-on": "bar-off";
    }
  },
  
  
};
</script>

<style>
.progress{
    height: 3px !important;
    opacity: 0.7 !important;
}
.bar-off{
  background-color: black !important;
}
.bar-on{
  background-color: #db524d !important;
}
.container {
  text-align: right;
  font-size: 8rem;
  width: 80%;
}
</style>
