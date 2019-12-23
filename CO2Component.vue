<!-- ---------------------------------------------------------------------- -->
<!-- COMPONENTE CO2 PARA TANQUE.
<!-- ---------------------------------------------------------------------- -->

<template>
	<v-container py-0>
		<!-- ================================================================== -->
		<!--  -->
		<!-- ================================================================== -->
		<v-layout align-center justify-center row fill-height class="alto326 ">
			<v-flex xs6 class="tuberias_co2_1" fill-height>
				<!-- Se muestra la botella CO2 de fondo -->
			</v-flex>
			<v-flex xs6 class="text-xs-center tuberias_co2_2" fill-height>
				<v-container
					fill-height
					align-center
					justify-center
					class="text-xs-center"
					pa-0
					ma-0
				>
					<ValvulaComponent
						sentido="up"
						:activo="VL"
						v-bind:texto="'VL-' + numero"
						posTexto="3"
					></ValvulaComponent>
				</v-container>
			</v-flex>
		</v-layout>

		<v-layout row>
			<v-flex xs6 class="text-xs-center tuberias_co2_3">
				<v-container align-center justify-center class="text-xs-center">
				
					<span class="frecuencia">{{ this.FREQ }}</span>

					<ValvulaComponent
						sentido="bomba"
						:activo="BOMBA"
						texto="BOMBA"
						posTexto="4"
					></ValvulaComponent>
				</v-container>
			</v-flex>

			<v-flex xs6 class="text-xs-center tuberias_co2_4">
				<v-container align-center justify-center class="text-xs-center">
					<ValvulaComponent
						sentido="left"
						:activo="VC"
						v-bind:texto="'VC-' + numero"
						posTexto="3"
					></ValvulaComponent>
				</v-container>
			</v-flex>
		</v-layout>

	</v-container>
</template>

<script>
import ValvulaComponent from "@/components/ValvulaComponent";
import DetectorComponent from "@/components/DetectorComponent";

export default {
	components: 
	{
		ValvulaComponent,
		DetectorComponent
	},

	props: 
	{
		// Por orden de aparición en el tanque.
		numero: Number, // Nº del tanque. 1..3
		VL: Boolean, // Válvula Llenado
		VC: Boolean, // Válvula Colector
		BOMBA: Boolean, // Bomba activa o no.
		FREQ: String	// Frecuencia de la bomba en 15/50Hz
	},

	data() {
		return {};
	}
};
</script>

<style scoped>

.alto326 {
	height: 326px;
}

.tuberias_co2_1 {
	/*background-image: url("../assets/camion/CO2tank.png"), url("../assets/camion/tuberia-hor-fijo.png");*/
	background-image: url("../assets/camion/co2.png"), url("../assets/camion/tuberia-hor-fijo.png");
	background-position: center, right center;
	background-repeat: no-repeat, no-repeat;
	background-size: auto, auto;
}

.tuberias_co2_2 {
	background-image: url("../assets/camion/tuberia-ver-fijo.png"), url("../assets/camion/tuberia-hor-fijo.png");
	background-position: center top, left center;
	background-repeat: no-repeat, no-repeat;
}

.tuberias_co2_3 {
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: center;
	background-repeat: repeat-x;
}

.tuberias_co2_4 {
	background-image: url("../assets/camion/tuberia-hor-fijo.png"), url("../assets/camion/tuberia-ver-fijo.png");
	background-position: left center, center -70%;
	background-repeat: no-repeat, no-repeat;
}

/* Desplazar el texto de para que se posicione sobre la bomba y no nos descuadre el resto de posiciones. */
.frecuencia
{
	position: absolute; 
	transform: translate(-68px, -25px);
}

</style>
