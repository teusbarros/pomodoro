<template>
  <div class="container">
    <div class="progress">
      <div
        class="progress-bar progress-bar-striped progress-bar-animated bg-success"
        role="progressbar"
        :aria-valuenow="{ percentage }"
        aria-valuemin="0"
        aria-valuemax="100"
        :style="{ width: percentage + '%' }"
      >{{percent}}%</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isConclued: this.conclued,
      percentage: this.percentual,
    };
  },
  props: {
    id: String,
    cor: String,
    percentual: Number,
    conclued: Boolean,
  },
  computed: {
    percent() {
      return this.percentage.toFixed();
    }
  },
  created() {
    var intval = setInterval(() => {
      if(this.percentage < 100)
        this.percentage += .01;
      else
        clearInterval(intval);
    }, 10);
  }
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
}
</style>
