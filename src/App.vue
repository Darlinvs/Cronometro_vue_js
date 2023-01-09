<template>

<div id="app">
<img src="./assets/cronometro.png" class="image">
<a class="timer">{{numero}}</a>

<div class="botoes">
  <button class="botao" @click="vai">{{botao}}</button>
  <button class="botao" @click="limpar">LIMPAR</button>
</div>

</div>

</template>

<script>
export default{
  name: 'App',
  data(){
    return{
      numero: 0,
      botao: 'VAI',
      timer: null,
      segundos:0,
      minutos:0,
      horas:0
    }
  },
  methods:{
    vai(){
      if(this.timer !== null){             //AQUI TEM ALGO RODANDO NO TIMER
       clearInterval(this.timer);
       this.timer = null;
       this.botao = 'VAI'
      }else{                               //AQUI O TIMER ESTÁ ZERADO OU PARADO
        this.timer = setInterval(() =>{
          this.rodarTimer();
        }, 1000);                          //VAI RODAR DE 1 EM 1 SEGUNDO
        this.botao = 'PAUSAR';
      }
    },
    //////////////////////////////////////////
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }
      this.segundos = 0;
      this.minutos = 0;
      this.horas = 0;
      this.numero = 0;
      this.botao = 'VAI';
    },
//////////////////////////////////////////////////////////
    rodarTimer(){
      this.segundos++;

      if(this.segundos == 59){
        this.segundos == 0;
        this.minutos++;
      }
      if(this.minutos == 59){
        this.minutos == 0;
        this.horas++
      }
      let format = (this.horas < 10 ? '0'+this.horas : this.horas) + ':'
      +(this.minutos < 10 ? '0'+this.minutos : this.minutos)+ ','
      +(this.segundos < 10 ? '0'+this.segundos : this.segundos);

      return this.numero = format;
    }
  }
}
</script>

<style>
#app{
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.image{
  width: 420px;
  height: 420px;
  padding-top: 100px;
}
.timer{
  font-size: 50px;
  margin-top: -145px;
}

.botoes{
  margin-top: 80px;
  display: flex;
}
.botao{
  -webkit-user-select: none;
  width: 150px;
  font-size: 15px;
  border: 0;
  border-radius: 10px;
  color: antiquewhite;
  background-color: rgb(15, 14, 14);
  padding: 5px;
  margin: 5px;
  cursor: pointer;
}

.botao:hover{
  opacity: 0.8;
  transition: all 0.58s;
}

</style>
