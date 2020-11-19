<template>
  <div class="container">
    <div class="progress" :class="animation">
      <div
        class="progress-bar progress-bar-striped progress-bar-animated"
        :class="bgBarra"
        role="progressbar"
        :aria-valuenow="{ percentual }"
        aria-valuemin="0"
        aria-valuemax="100"
        :style="{ width: percentual + '%' }"
      >{{percentual}}%</div>
    </div>
  </div>
</template>

<script>
export default {
  computed:{
    animation: function () {
      if (this.workTime) {
        return 'bounce-enter';
      }else{
        return 'bounce-leave'
      }
    }, 
    bgBarra: function () {
      if (this.workTime) {
        return 'bg-barra-enter';
      }else{
        return 'bg-barra-leave'
      }
    }
  },
  props: {
    percentual: Number,
    workTime: Boolean
  },
  
};
</script>

<style scoped>

.progress{
    height: 50px !important;
    /* opacity: 1; */
}
.container {
  text-align: right;
  font-size: 8rem;
  color: #555;
  width: 80%;
}
.bg-worktime{
  background-color: #db524d;
}
/* animações */
.bounce-enter {
  background-color: #db524d;
  animation: bounce-in .5s;
}
.bounce-leave {
  background-color: #4ddb4d;
  animation: bounce-out .5s;
}
.bg-barra-enter{
  background-color: #4ddb4d;
  /* background-image: url("../../public/t2.png"); */
}
.bg-barra-leave{
  background-color: #db524d;
  /* background-image: url("../../public/t2.png"); */
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes bounce-out {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(0);
  }
}
</style>
