<template>
  <div class="container">
    <div class="progress" :class="animation">
      <div
        class="progress-bar progress-bar-striped progress-bar-animated bg-worktime"
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
  data() {
    return {
      animation: 'bounce-enter',
    };
  },
  props: {
    id: String,
    percentual: Number,
    conclued: Boolean,
    started: Boolean
  },
  
};
</script>

<style scoped>
.progress{
    height: 50px !important;
}
.container {
  text-align: right;
  font-size: 8rem;
  color: #555;
  width: 80%;
}
.bg-worktime{
  background-color: rgb(219, 82, 77);
}
/* animações */
.bounce-enter {
  animation: bounce-in .5s;
}
.bounce-leave {
  animation: bounce-out .5s;
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
