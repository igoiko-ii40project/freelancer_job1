<!-- ---------------------------------------------------------------------- -->
<!-- COMPONENTE VÁLVULA PARA TANQUE -->
<!-- Válidos para VA, VL, VC -->
<!-- ---------------------------------------------------------------------- -->

<template>
  <div v-bind:class="'posIcon' + posTexto">
    <div class="title desplazar" v-bind:class="'posTexto' + posTexto">
      {{ texto }}
    </div>
    <v-icon
      class="valvula elevation-10"
      color="#fff"
      size="50px"
      v-bind:class="[activo ? 'activa' : 'no-activa']"
      >{{ caracter }}</v-icon
    >
  </div>
</template>

<script>
export default {
  props: {
    activo: Boolean, // Valor de la válvula.
    sentido: String, // Sentido de la flecha: up, down, left
    texto: String, // Texto o nombre de la válvula.
    posTexto: String // Posición del texto: 1(izquierda-abajo), 2(derecha-arriba), 3(derecha-centrado).
  },

  data() {
    // Siempre tiene que haber un texto
    var miCar = "clear";

    if (this.sentido == "up") miCar = "arrow_upward";
    else if (this.sentido == "down") miCar = "arrow_downward";
    else if (this.sentido == "left") miCar = "arrow_back";
    else if (this.sentido == "bomba") miCar = "fast_rewind";

    return {
      caracter: miCar
    };
  }
};
</script>

<style scoped>
.valvula {
  border-radius: 50%;
  border: 5px solid rgba(50, 50, 50, 0.6);
  background-color: rgba(
    50,
    50,
    50,
    0.6
  ); /* color de fondo en caso de que no haya valor para la válvula. */
}

.activa {
  background-color: lightgreen;
}

.no-activa {
  background-color: crimson;
}

.desplazar {
  height: 0;
}

.posIcon1 {
  transform: translate(0, 20px);
}

/* .posIcon2
{
	transform: translate( 0, 20px);
} */

/* .posIcon3
{
	transform: translate( 0, -50px);
} */

/* Texto izquierda-abajo*/
.posTexto1 {
  transform: translate(-55px, 35px);
}

/* Texto Derecha-arriba*/
.posTexto2 {
  transform: translate(55px, 5px);
}

/* Texto derecha-en medio*/
.posTexto3 {
  transform: translate(55px, 20px);
}

/* Abajo centrado */
.posTexto4 {
  transform: translate(0, 60px);
}
</style>
