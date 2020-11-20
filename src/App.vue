<template>
  <div id="app">
    <Navbar :workTime="workTime"></Navbar>
    <div class="barras">
      <Barra :percentual="barTime" :workTime="workTime"></Barra>
    </div>
    <h1 class="time" :class="bgCor">{{ showMinutos }}:{{ showSegundos }}</h1>
    <div class="botoes">
      <Botao nome="INICIAR" :cor="bgCor" :acao="iniciar"></Botao>
      <Botao nome="PARAR" :cor="bgCor"  :acao="parar" v-if="!stop"></Botao>
      <Botao nome="CONTINUAR" :cor="bgCor"  :acao="parar" v-else></Botao>
      <Botao nome="TRABALHO" :cor="bgCor" :acao="work" v-if="!workTime"></Botao>
      <Botao nome="DESCANSO" :cor="bgCor" :acao="work" v-else></Botao>
    </div>
    <div class="ajuda">

    </div>
  </div>
</template>

<script>
import Barra from "./components/Barra.vue";
import Navbar from "./components/Navbar.vue";
import Botao from "./components/Botao.vue";

export default {
  name: "App",
  components: {
    Barra,
    Navbar,
    Botao
  },
  data() {
    return {
      workMinutes: 25,
      restMinutes: 5,
      minutos: 25,
      segundos: 0,
      stop: false,
      workTime: true,
      interval: '',
      counting: false,
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
    },
    bgCor:function () {
        return this.workTime ? "bg-on": "bg-off";
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
            this.sirene();
            this.work();
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
        clearInterval(this.interval);
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
    sirene: function () {
        var audio = new Audio(require('../public/beep.mp3'));
        audio.play();
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
  background-color: #e2e2e2;
  height: 100%;
}
.time {
  font-size: 150px;
  margin-bottom: 25px;
}
.barras {
    width: 55%;
    margin: auto;
}

.botoes{
  padding-bottom: 220px;
}
.bg-on{
    border-color: #db524d;
    color: #db524d;
}
.bg-off{
    border-color: #000;
    color: #000;
}
</style>
