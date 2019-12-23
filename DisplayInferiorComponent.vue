<!-- ---------------------------------------------------------------------- -->
<!-- COMPONENTE DISPLAY INFERIOR TANQUE PARA CERVEZA
<!-- ---------------------------------------------------------------------- -->

<template>
  <v-container fluid py-0 px-0 grid-list-md>
    <v-layout row class="display text-xs-center">
      <v-flex xs4>
        <v-card-text class="elevation-5 fondo">
          Presión Colector<br />
          <h2>{{ precol }}</h2>
        </v-card-text>
      </v-flex>
      <v-flex xs4>
        <v-card-text class="elevation-5 fondo">
          Temperatura Ambiente<br />
          <h2>{{ temamb }}</h2>
        </v-card-text>
      </v-flex>
      <v-flex xs4>
        <v-card-text class="elevation-5 fondo">
          Presión Neumática<br />
          <h2>{{ preneu }}</h2>
        </v-card-text>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  props: {
    precol: String, // Presión colector
    temamb: String, // Temperatura ambiente
    preneu: String // Presión neumática
  },

  data() {
    return {};
  }
};
</script>

<style scoped>
.display .fondo {
  color: white;
  /* background-color: #315a58; */
  background-color: #315a58;
}

.fondo {
  /* background-color: #315a58; */
}
</style>
