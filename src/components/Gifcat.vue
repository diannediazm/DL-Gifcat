<template>
  <div>
    <h1>Random Gif Cat</h1>
    <form @submit.prevent="buscarGato">
      <div>
        <label for="titulo">Título: </label>
        <input type="titulo" v-model="titulo">
      </div>
      <br>
      <div>
        <label>Filtro: </label>
        <select v-model="filtro">
          <option>blur</option>
          <option>mono</option>
          <option>sepia</option>
          <option>negative</option>
          <option>paint</option>
          <option>pixel</option>
        </select>
      </div>
      <br>
       <div>
        <label>Color: </label> 
        <select v-model="color">
          <option>red</option>
          <option>blue</option>
          <option>green</option>
          <option>orange</option>
          <option>yellow</option>
        </select>
         <span class="circulo"></span>
      </div>
      <br>
      <div>
        <label for="size">Tamaño: </label>
        <input type="size" v-model="size">
      </div>
      <br>
      <button type="submit" v-on:click="validar">Obtener gatito</button>
    </form>
    <section class="resultado">
      <img :src="imagen" alt="">
    </section>
  </div>
</template>

<script>
export default {
  name: 'Gifcat',
  data() {
    return {
      titulo: '',
      filtro: '',
      color: '',
      size: '',
      imagen: ''
    }
  },
  methods: {
    validar() {
      if (this.titulo === '') {
        alert('Favor, escriba un título');
        return false;
      }
      else if (this.filtro === '') {
        alert('Favor, elija un filtro');
        return false;
      }
      else if (this.color === '') {
        alert('Favor, elija un color');
        return false;
      }
      else if (this.size === '') {
        alert('Determine un tamaño en pixeles');
        return false;
      }
      else if (isNaN(this.size)) {
        alert('En tamaño incluir solo números');
        return false;
      }
    },
    buscarGato(){
      fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.size}`)
      .then(result => {
        console.log(result);
        this.imagen = result.url;
      });
    }
  }
}
</script>


<style scoped>
h1 {
  text-align: center;
  background-color: lightblue;
  font-family: Arial, Helvetica, sans-serif;
  padding-top: 80px;
  padding-bottom: 40px;
  margin: 0px;  
}
form {
  background-color: lightsalmon;
  padding-top: 20px;
  padding-bottom: 20px;
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
  display: block;
}
.resultado {
  text-align: center;
  background-color: lightblue;
  font-family: Arial, Helvetica, sans-serif;
  padding-top: 20px;
  padding-bottom: 300px;
  margin: 0px;
}
.circulo {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: red;
  display: inline-block;
  margin-left: 10px;
}
</style>
