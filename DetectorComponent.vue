<!-- ---------------------------------------------------------------------- -->
<!-- COMPONENTE DETECTOR PARA TANQUE -->
<!-- Válidos para DETECTORES de lleno y vacío -->
<!-- ---------------------------------------------------------------------- -->

<template>

	<v-icon 
		size="50px" 
	class="detector" 
	v-bind:class="[activo ? 'activa' : '']"
	>
		fiber_manual_record
	</v-icon>

</template>

<script>
export default {
	props: {
		activo: Boolean // Valor del detector.
	},

	data() {
		return {};
	}
};
</script>

<style scoped>
.detector {
	color: #ccc;
	border-radius: 50%;
	background-color: rgba(50, 50, 50, 0.6);
	margin: 15px 0;
}

.activa {
	color: lightgreen;
}
</style>
