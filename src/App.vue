<template>
  <div id="app">
    <Navbar></Navbar>
    <div class="barras">
      <Barra :percentual="barTime" :conclued="false"></Barra>
    </div>
    <h1 class="time">{{ showMinutos }}:{{ showSegundos }}</h1>
    <div>
      <button class="btn btn-success" @click="iniciar">INICIAR</button>
      <button class="btn btn-danger" @click="parar" v-if="!stop">PAUSAR</button>
      <button class="btn btn-danger" @click="parar" v-else>CONTINUAR</button>
      <button class="btn btn-primary" @click="zerar">ZERAR</button>
      <button class="btn btn-warning" @click="work" v-if="!workTime">TRABALHO</button>
      <button class="btn btn-warning" @click="work" v-else >DESCANSO</button>

    </div>
  </div>
</template>

<script>
import Barra from "./components/Barra.vue";
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: {
    Barra,
    Navbar,
  },
  data() {
    return {
      workMinutes: 25,
      restMinutes: 5,
      minutos: 25,
      segundos: 0,
      stop: false,
      workTime: false,
      interval: '',
      counting: false
    };
  },
  computed: {
    showSegundos: function(){
      return this.segundos < 10 ? "0" + this.segundos: this.segundos;
    },
    showMinutos: function(){
      return this.minutos < 10 ? "0" + this.minutos: this.minutos;
    },
    barTime: function(){
      if (!this.counting) {
        return 0;
      }
      var complete = this.minutos * 60;
      complete = complete + this.segundos;
      if (this.workTime) {
        return 100 - (complete/(this.workMinutes*60) * 100).toFixed();
      }else{
        return 100 - (complete/(this.restMinutes*60) * 100).toFixed();
      }
    }
  },
  methods: {
    decreaseTime: function () {
      if (!this.stop) {
        if (this.segundos == 0) {
          if (this.minutos > 0) {
            this.minutos--;
            this.segundos = 59;
          }else{
            // this.workTime = !this.workTime;
            // o tempo acabou! fazer algo
            // todo: alternar tempo automaticamente
          }
        } else {
          this.segundos--;
        }
        this.showMinutos =
          this.minutos < 10 ? "0" + this.minutos : this.minutos;
        this.showSegundos =
          this.segundos < 10 ? "0" + this.segundos : this.segundos;
      }
    },
    setTime:function(work = false){
      if (this.workTime || work) {
        this.minutos = this.workMinutes;
        this.segundos = 0;
      }else{
        this.minutos = this.restMinutes;
        this.segundos = 0
      }
    },
    iniciar: function () {
      // this.segundos--;
      this.setTime();
      this.stop = false;
      this.counting = true;
      this.interval = setInterval(this.decreaseTime, 1000);
    },
    parar: function () {
      this.stop = !this.stop;
    },
    work: function () {
      this.workTime = !this.workTime;
      clearInterval(this.interval);
      this.setTime();
    },
    zerar: function () {
      this.workTime = true;
      clearInterval(this.interval);
      this.setTime();
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
.time {
  font-size: 150px;
  margin-bottom: 100px;
}
.barras {
  margin-top: 100px;
}
.btn {
  width: 150px;
  margin: 0 30px 0 30px;
}
</style>
