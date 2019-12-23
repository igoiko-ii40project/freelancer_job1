<!-- ---------------------------------------------------------------------- -->
<!-- COMPONENTE TANQUE PARA CERVEZA
<!-- Se inserta en un grid y ocupa 2 columnas. 
<!-- ---------------------------------------------------------------------- -->

<template>
  <v-container class="tank" py-0>
    <!-- ================================================================== -->
    <!-- Línea para VA y VL -->
    <!-- ================================================================== -->
    <v-layout row class="xxtank-top">
      <v-flex xs6 class="text-xs-center">
        <ValvulaComponent
          sentido="up"
          :activo="VA"
          v-bind:texto="'VA-' + numero"
          posTexto="1"
        ></ValvulaComponent>
      </v-flex>
      <v-flex xs6 class="text-xs-center XXtuberia_vert">
        <ValvulaComponent
          sentido="down"
          :activo="VL"
          v-bind:texto="'VL-' + numero"
          posTexto="2"
        ></ValvulaComponent>
      </v-flex>
    </v-layout>

    <!-- ================================================================== -->
    <!-- Línea para DETEC. LLENO TANQUE -->
    <!-- ================================================================== -->
    <v-layout row>
      <v-flex xs12 class="text-xs-right tank-top">
        <DetectorComponent :activo="DL"></DetectorComponent>
      </v-flex>
    </v-layout>

    <!-- ================================================================== -->
    <!-- DATOS del tanque -->
    <!-- ================================================================== -->
    <v-layout row>
      <v-flex xs12 class="text-xs-center title tank-center">
        <div class="visualizadorDatos">
          {{ nombre }}<br />
          {{ tipo }}<br />
          {{ temperatura }}<br />
          {{ presion }}<br />
          {{ cantidad }}<br />
        </div>
      </v-flex>
    </v-layout>

    <!-- ================================================================== -->
    <!-- Línea para DETEC. VACIO TANQUE -->
    <!-- ================================================================== -->
    <v-layout row>
      <v-flex xs12 class="text-xs-right tank-bottom">
        <DetectorComponent :activo="DV"></DetectorComponent>
      </v-flex>
    </v-layout>

    <!-- ================================================================== -->
    <!-- Línea para VC -->
    <!-- ================================================================== -->
    <v-layout row>
      <v-flex xs12 class="text-xs-center zztuberia_hor_m">
        <ValvulaComponent
          sentido="down"
          :activo="VC"
          v-bind:texto="'VC-' + numero"
          posTexto="3"
        ></ValvulaComponent>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import ValvulaComponent from "@/components/ValvulaComponent";
import DetectorComponent from "@/components/DetectorComponent";

export default {
  components: {
    ValvulaComponent,
    DetectorComponent
  },

  props: {
    // Por orden de aparición en el tanque.
    numero: Number, 		// Nº del tanque. 1..3
    nombre: String, 		// Nombre del tanque
    VA: Boolean, 			// Válvula Aire
    VL: Boolean, 			// Válvula Llenado
    DL: Boolean, 			// Detector Lleno
    tipo: String, 			// Tipo de cerveza
    temperatura: String,
    presion: String,
    cantidad: String,
	cantidaddia: String,	// Cantidad suministrada por día.
    DV: Boolean, 			// Detector Vacío
	VC: Boolean, 			// Válvula Colector
  },

  data() {
    return {};
  }
};
</script>

<style scoped>
.tank {
  /* Evitar desajustes en los tamaños. */

  max-width: 319px; /* 398x80% */
}

.tank-top {
  background-image: url("../assets/camion/Deposito-top.png");
  background-position: bottom;
  background-size: 80%;
  /* background-repeat: repeat-y;   */
}

.tank-center {
  /*background-image: url("../assets/camion/tank-center.png");*/
  background-image: url("../assets/camion/Deposito-center.png");
  background-position: bottom;   /* was center*/
  background-size: contain;
  background-repeat: repeat-y;
}

.tank-bottom {
  background-image: url("../assets/camion/Deposito-bottom.png");
  background-position: top;
  background-size: 80%;
  /* background-repeat: repeat-y; */
}

/*  background-color: rgb(255, 255, 255, 0.6);*/
.visualizadorDatos {
  /*background-color: rgb(255, 255, 255, 0.6);*/
  background-color:"";
  opacity: "";
  width: 60%;
  margin: auto;
  border-radius: 15px;
  color:white;
  font:"italic bold 10px arial,serif";
}
</style>
