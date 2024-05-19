<template>
  <div id="app">
    <h1 class="text-center py-3">Modifica el Cuadrado</h1>
    <main class="container">
      <div class="row align-items-center">
        <section class="col col-md-12 col-lg-4">
          <form class="container">
            <div class="d-flex align-items-center py-2">
              <label class="px-2" for="colorFondo">Color de fondo</label>
              <input type="color" name="colorFondo" id="colorFondo" v-model="colorFondo">
            </div>
            <div class="d-flex align-items-center py-2">
              <label class="px-2" for="colorTexto">Color de texto</label>
              <input type="color" name="colorTexto" id="colorTexto" v-model="colorTexto">
            </div>
            <div class="d-flex align-items-center py-2">
              <label class="px-2" for="mostrarTexto">Mostar texto</label>
              <input type="checkbox" name="mostrarTexto" id="mostrarTexto" v-model="mostrarTexto">
            </div>
            <div class="row py-2 px-2">
              <label for="rangeRadius">Borde</label>
              <input type="range" name="rangeRadius" id="rangeRadius" min="10" max="50" v-model="rangeRadius">
            </div>
            <div class="row py-2 px-2">
              <label for="contenidoTexto">Contenido textual</label>
              <textarea name="contenidoTexto" id="contenidoTexto" placeholder="Escribe tu texto aquí"
                v-model="contenidoTexto"></textarea>
            </div>
            <div class="d-flex align-items-center py-2">
              <label class="px-2" for="tipoTipografia">Típografia</label>
              <select name="tipoTipografia" id="tipoTipografia" v-model="tipoTipografia">
                <option v-for="(tipografia, index) in tipografias" :key="index" :value="tipografia.font">{{
                  tipografia.name
                  }}</option>
              </select>
            </div>
            <div class="d-flex align-items-center py-2">
              <label class="px-2" for="opacidad">Opaco</label>
              <input type="checkbox" name="opacidad" id="opacidad" v-model="opacity">
            </div>
            <div class="row py-2 px-2">
              <label for="">Tamaño de letra</label>
              <div>
                <input class="mx-1" type="radio" value="Pequeño" v-model="tamañoLetra">Pequeño
                <input class="mx-1" type="radio" value="Mediano" v-model="tamañoLetra">Mediano
                <input class="mx-1" type="radio" value="Grande" v-model="tamañoLetra">Grande
              </div>
            </div>
          </form>
        </section>
        <section class=" col-md-12 col-lg-4 py-5 ">
          <div :class="{ boxResultado: true }" :style="{ backgroundColor: color2(), borderRadius: rangeRadius + 'px' }">
            <div v-show="mostrarTexto" >
              <div class=" d-flex align-items-center justify-content-center box-texto">
                <p class="" v-if="tamañoLetra == 'Pequeño'"
                  :style="{ fontFamily: tipoTipografia, fontSize: '1.5em', color: colorTexto, textAlign:'center' }">{{ contenidoTexto }}</p>
                <p v-else-if="tamañoLetra == 'Mediano'"
                  :style="{ fontFamily: tipoTipografia, fontSize: '2.5em', color: colorTexto }">{{ contenidoTexto }}</p>
                <p v-else :style="{ fontFamily: tipoTipografia, fontSize: '3.5em', color: colorTexto }">{{ contenidoTexto
                  }}</p>
              </div>
            </div>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      colorFondo: '',
      colorTexto: '',
      mostrarTexto: false,
      rangeRadius: '',
      contenidoTexto: '',
      opacity: false,
      tipoTipografia: '',
      tamañoLetra: '',
      tipografias: [
        { name: 'Open Sans', font: '"Open Sans", sans-serif' },
        { name: 'Yellowtail', font: '"Yellowtail", cursive' },
        { name: 'Young Serif', font: '"Young Serif", serif' },
        { name: 'Over the Rainbow', font: '"Over the Rainbow", cursive' }
      ]
    }
  },
  methods: {
    color2: function () {
      console.log(this.colorFondo)
      let red = parseInt(this.colorFondo.slice(1, 3), 16)
      let green = parseInt(this.colorFondo.slice(3, 5), 16)
      let blue = parseInt(this.colorFondo.slice(5, 7), 16)
      let transparencia = 0.7
      if (this.opacity) {
        transparencia = 1
      }
      console.log(red)
      return `rgba(${red},${green},${blue},${transparencia})`
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&family=Over+the+Rainbow&family=Yellowtail&family=Young+Serif&display=swap');

/* #app{
  margin: 0 10%;
} */
.boxResultado {
  width: 100%;
  height: 50vh;
  background-color: transparent;
}

form {
  /* width: 350px;
  height: 450px; */
  background-color: rgb(65, 5, 177);
  color: white;
  border-radius: 22px;
  padding: 10px 10px;
}

.box-texto {
  width: 100%;
  height: 50vh;
  overflow: hidden;
}

.texto {
  width: 350px;
  height: 350px;
}
</style>
