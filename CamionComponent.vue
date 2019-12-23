<template>
	<v-container fluid class="minimo">
		<v-layout row wrap justify-center>
			<v-flex xs2 text-xs-center>
				
				<!-- 👉 El botón con My Location: clicando en la matricula para que salga el mapa-->  
				<!-- <v-btn :to="'/mapa/' + deviceName" color="#f29e3e" dark><v-icon>my_location</v-icon></v-btn> -->
				
				<v-btn :to="{path:'/mapalocal/' + deviceName+'/'+deviceCoords+'/16', params: { deviceName: deviceName, deviceCoords: deviceCoords, zoom_in:16 }}" flat color="#f29e3e" dark>
					<div class="display-1 naranja">{{ deviceName }}</div>
				</v-btn>

			</v-flex>			
		</v-layout>

		<v-layout row wrap justify-space-around>
			<v-flex xs3 text-xs-left justify-between>
				<!-- <v-card outlined=true color="red" :style="{color: (parseInt(this.datosAlarmas.length,10) >1)?'red':'white'}">
					<v-card-text :style="{color: (parseInt(this.datosAlarmas.length,10) >1)?'white':'black'}">	
						<div class="contenedor">
							<div class="flex-item anchoFijo" font-size="8px"><v-icon :style="{color: (parseInt(this.datosAlarmas.length,10) >1)?'white':'black'}">notification_important</v-icon>{{ this.datosAlarmas[0] }}</div>
							<v-btn flat small color="error">VER TODAS</v-btn>
						</div>
					</v-card-text>
				</v-card> -->
				<!-- <span v-if="(parseInt(this.datosAlarmas.length,10) >1)"> -->
				<span v-if="( this.datosAlarmas[0] !== 'No active alarms' )">
					<v-card outlined=true color="rgba(255, 0, 0, 0.5)" disabled="true">
						<v-card-text color='white'>	<!--class="elevation-5 fondo"-->
							<div class="contenedor">
								<div class="flex-item anchoFijo" fontSize="8px" color='white'><v-icon color='white'>notification_important</v-icon>{{ this.datosAlarmas[0] }}</div>
								
								<v-btn flat small color="white" href="#alarmas">VER TODAS</v-btn> <div color='white'>of {{this.datosAlarmas.length}} </div>
							</div>
						</v-card-text>
					</v-card>
					</span>
				<span v-else>
					<v-card outlined=true color="white">
						<v-card-text color='black'>	<!--class="elevation-5 fondo"-->
							<div class="contenedor">
								<div class="flex-item anchoFijo" fontSize="8px"><v-icon color='black'>thumb_up</v-icon>{{ this.datosAlarmas[0] }}</div>
								<div>{{this.datosAlarmas.length}} </div>
							</div>
						</v-card-text>
					</v-card>
					</span>
			</v-flex>

			<v-flex xs3 text-xs-left justify-space-around>		<!--/*<v-flex xs2 text-xs-left body-2> */-->

				<div class="contenedor">
					<div class="flex-item anchoFijo" fontSize="8px" :style="{color: ( this.isOnline === 'online')?'blue':'black', opacity: ( this.isOnline === 'online')?'1':'0.5' }"><v-icon :style="{color: ( this.isOnline === 'online')?'blue':'black'}">wifi_tethering</v-icon>Últ. Conexión:</div>		<!-- icons library: https://material.io/resources/icons/?style=baseline -->
					<div class="flex-item" fontSize="8px" :style="{color: ( this.isOnline === 'online')?'blue':'black', opacity: ( this.isOnline === 'online')?'1':'0.5' }">{{ this.ultimaLectura }}</div>
					</div>

				<!-- 👉 Si el texto de la alarma es vacío, no se pinta nada. 
				No he puesto el v-show pq no me guardaba el hueco. De esta manera guarda el hueco.-->
				<!-- <div class="contenedor" :style="{visibility: this.txtAlarma ? 'visible' : 'hidden'}">
					<div class="flex-item anchoFijo">Alarma:</div>
					<div class="flex-item">{{ this.txtAlarma }}</div>
				</div> -->

				<span v-if="datosCamion && datosCamion['SISTEMA MAN/AUTO']">
					<!-- <div><span class="mdi-auto-fix" font-size="16px"></span>Automatico</div></span> -->
					<!-- <div fontSize="8px" :style="{opacity: ( this.isOnline === 'online')?'1':'0.5'}"><v-icon >loop</v-icon>Automatico</div></span> -->
					<div fontSize="8px" v-bind:class="{ offline: !isOnline }"><v-icon >loop</v-icon>Automatico</div></span>
				<span v-else>
					<!-- <div><span class="mdi-hand-right" font-size="16px"></span>Manual</div> -->
					<div fontSize="8px" v-bind:class="{ offline: !isOnline }"><v-icon >pan_tool</v-icon>Manual</div></span>
			</v-flex>
			
			<v-flex xs2 text-xs-left justify-between>	<!--/*<v-flex xs2 text-xs-left body-2> */-->
				<span v-if="datosCamion && datosCamion['CONEXION BATERIA/ENCHUFADO']">
					<!-- <div><span class="mdi-power-plug"></span>Enchufado</div> -->
					<div v-bind:class="{ offline: !isOnline }"><v-icon >power</v-icon>{{ this.datosCamion['CONEXION BATERIA/ENCHUFADO'] }}</div></span>
				<span v-else>
					<!-- <div><span class="mdi-battery-medium"></span>Bateria</div> -->
					<div v-bind:class="{ offline: !isOnline }"><v-icon >battery_std</v-icon>Bateria</div></span>

 
				<div>
				<span
					v-if="datosCamion && datosCamion['SETA DE EMERGENCIA']"
					class="seta seta_activa pa-1 blink_me_icon"
				>
					<v-icon color="red" class="seta">adjust</v-icon>	<!-- icon was: warning -->
					<span class="blink_me">EMERGENCIA</span>
				</span>
				<span v-else class="seta seta_inactiva pa-1">
					<v-icon color="#eee" class="seta">adjust</v-icon>EMERGENCIA
				</span>
				</div>

			</v-flex>

			<!-- <v-flex xs2 text-xs-center>
				<v-btn :to="{path:'/mapalocal/' + deviceName+'/'+deviceCoords+'/16', params: { deviceName: deviceName, deviceCoords: deviceCoords, zoom_in:16 }}" flat color="#f29e3e" dark>
					<div class="display-1 naranja">{{ deviceName }}</div>
				</v-btn>
			</v-flex> -->

			<!-- <v-flex xs2 text-xs-right>

			</v-flex> -->

			<v-flex xs2 justify-between>
				<DialogOperadorComponent
					v-bind:codigo	= "this.datosCamion['CODIGO OPERADOR']"
					v-bind:nombre	= "this.datosCamion['NOMBRE OPERADOR']"
					v-bind:pila		= "this.datosCamion['NOMBRE PILA OPERADOR']"
					v-bind:telefono	= "this.datosCamion['TELEFONO OPERADOR']"
				/>
				<br />
				<!-- <span
					v-if="datosCamion && datosCamion['SETA DE EMERGENCIA']"
					class="seta seta_activa pa-1 blink_me_icon"
				>
					<v-icon color="white" class="seta">warning</v-icon>
					<span class="blink_me">EMERGENCIA</span>
				</span>
				<span v-else class="seta seta_inactiva pa-1">
					<v-icon color="#eee" class="seta">warning</v-icon>EMERGENCIA
				</span> -->



			</v-flex>

		</v-layout>
		<v-divider class="pb-2" />

		<!-- ============================================================== -->
		<!-- == GRID PARA LAS 4 COLUMNAS. -->
		<!-- ============================================================== -->

		<v-layout row wrap>
			<v-flex xs1 class="tuberia_hor_degr"> </v-flex>
			<v-flex xs11 class="tuberia_hor_b">
				&nbsp;
			</v-flex>
		</v-layout>

		<v-layout row wrap>
			<v-flex xs3>

				<CO2Component
					:numero="4"
					v-bind:VL="this.datosCamion['VALV. LLENADO SUMINISTRO']"
					v-bind:VC="this.datosCamion['VALV. COLECTOR SUMINISTRO']"
					v-bind:BOMBA="this.datosCamion['BOMBA ON/OFF']"
					v-bind:FREQ="this.datosCamion['FREQUENCIA 15/50Hz']"
				>
				</CO2Component>
			</v-flex>
			<v-flex xs3 class="tuberias_tank">
				<TankComponent
					:numero="3"
					v-bind:nombre		="this.datosCamion['NOMBRE TANQUE_03']"
					v-bind:VA			="this.datosCamion['VALV. AIRE TANQUE_03']"
					v-bind:VL			="this.datosCamion['VALV. LLENADO TANQUE_03']"
					v-bind:VC			="this.datosCamion['VALV. COLECTOR TANQUE_03']"
					v-bind:DL			="this.datosCamion['DETEC. LLENO TANQUE_03']"
					v-bind:DV			="this.datosCamion['DETEC. VACIO TANQUE_03']"
					v-bind:tipo			="this.datosCamion['TIPO TANQUE_03']"
					v-bind:temperatura	="this.datosCamion['TEMP TANQUE_03']"
					v-bind:presion		="this.datosCamion['PRES TANQUE_03']"
					v-bind:cantidad		="this.datosCamion['CANT TANQUE_03']"
					v-bind:cantidaddia	="this.datosCamion['CANTIDAD SUMIN TANQUE_03']"
				>
				</TankComponent>
			</v-flex>
			<v-flex xs3 class="tuberias_tank">
				<TankComponent
					:numero="2"
					v-bind:nombre		="this.datosCamion['NOMBRE TANQUE_02']"
					v-bind:VA			="this.datosCamion['VALV. AIRE TANQUE_02']"
					v-bind:VL			="this.datosCamion['VALV. LLENADO TANQUE_02']"
					v-bind:VC			="this.datosCamion['VALV. COLECTOR TANQUE_02']"
					v-bind:DL			="this.datosCamion['DETEC. LLENO TANQUE_02']"
					v-bind:DV			="this.datosCamion['DETEC. VACIO TANQUE_02']"
					v-bind:tipo			="this.datosCamion['TIPO TANQUE_02']"
					v-bind:temperatura	="this.datosCamion['TEMP TANQUE_02']"
					v-bind:presion		="this.datosCamion['PRES TANQUE_02']"
					v-bind:cantidad		="this.datosCamion['CANT TANQUE_02']"
					v-bind:cantidaddia	="this.datosCamion['CANTIDAD SUMIN TANQUE_02']"
				>
				</TankComponent>
			</v-flex>
			<v-flex xs3 class="tuberias_tank">
				<TankComponent
					:numero="1"
					v-bind:nombre		="this.datosCamion['NOMBRE TANQUE_01']"
					v-bind:VA			="this.datosCamion['VALV. AIRE TANQUE_01']"
					v-bind:VL			="this.datosCamion['VALV. LLENADO TANQUE_01']"
					v-bind:VC			="this.datosCamion['VALV. COLECTOR TANQUE_01']"
					v-bind:DL			="this.datosCamion['DETEC. LLENO TANQUE_01']"
					v-bind:DV			="this.datosCamion['DETEC. VACIO TANQUE_01']"
					v-bind:tipo			="this.datosCamion['TIPO TANQUE_01']"
					v-bind:temperatura	="this.datosCamion['TEMP TANQUE_01']"
					v-bind:presion		="this.datosCamion['PRES TANQUE_01']"
					v-bind:cantidad		="this.datosCamion['CANT TANQUE_01']"
					v-bind:cantidaddia	="this.datosCamion['CANTIDAD SUMIN TANQUE_01']"
				>
				</TankComponent>
			</v-flex>
		</v-layout>

		<v-layout row wrap>
			<v-flex xs12 class="tuberia_hor_t">
				&nbsp;
			</v-flex>
		</v-layout>

		<DisplayInferiorComponent
			v-bind:precol ="this.datosCamion['PRES COLECTOR']"
			v-bind:temamb ="this.datosCamion['TEMP DEL AMBIENTE']"
			v-bind:preneu ="this.datosCamion['PRES NEUMATICA']"
		>
		</DisplayInferiorComponent>

		<v-divider class="pb-4" />

		<v-layout row wrap justify-center>
			<v-flex xs12 md12>
				<GraficoLineComponent
					grafico			 = "Plot_1"
					v-bind:deviceUrl = "this.deviceUrl"
					v-bind:deviceID  = "this.deviceID"
					v-bind:selectable_vars_for_plot = "this.selectable_vars_for_plot1"
					v-bind:show_selectable_vars = "this.show_selectable_vars"
				/>
			</v-flex>
		</v-layout>

		<div id="alarmas"></div>
		<v-layout row wrap justify-center>
			<v-flex xs12 md12>
				<AlarmasComponent 		 v-bind:deviceUrl="this.deviceUrl" v-bind:deviceID="this.deviceID" />
			</v-flex>
		</v-layout>

		<v-layout row wrap justify-center>
			<v-flex xs12 md12>
				<NotificacionesComponent v-bind:deviceUrl="this.deviceUrl" v-bind:deviceID="this.deviceID" />
			</v-flex>
		</v-layout>

		<v-layout row wrap justify-center>
			<v-flex xs12 md12>
			<RutaComponent2				v-bind:deviceUrl="this.deviceUrl"	v-bind:deviceID="this.deviceID" />
			</v-flex>
		</v-layout>

		<v-layout row wrap justify-space-around>
			<v-flex xs8 md8>
				<!-- <h1>Ruta Camión</h1> -->
				<TravelRutaComponent 	v-bind:deviceUrl="this.deviceUrl"	
										v-bind:deviceID="this.deviceID" 
										v-bind:deviceCoords="this.deviceCoords" 
										v-bind:deviceCoords_datestamp="this.deviceCoords_datestamp" 
										v-bind:Map_PdVs="this.this_PdVs" 
										class="travel-map"/>
			</v-flex>
			<v-flex xs3 md3>
				<!-- <h1>Consulta de Ruta</h1> -->
				<!-- Vuetify -->
				<v-form>
					<!--<v-text-field label="Itinerary_name" type="text" />		-->
					<v-text-field
						v-model="itinerary_day"
						label="Fecha para Consultar Ruta"
						prepend-icon="event"
						readonly
						v-on="on"
					></v-text-field>
					<v-date-picker 
						v-model="itinerary_day" 
						locale="es"
						:first-day-of-week="1"
						no-title 
						@input="showMenuDateFin = false"
					></v-date-picker>
					<v-btn color="#f29e3e" dark v-on="on" @click="consultarRuta"><v-icon dark left>insert_chart_outlined</v-icon>Consultar Ruta</v-btn>
				</v-form>			
			</v-flex>
		</v-layout>

		<v-layout row wrap justify-center>
			<v-flex xs12 md12>
			<OpsSummaryComponent 	v-bind:deviceUrl="this.deviceUrl" 
									v-bind:deviceID="this.deviceID" 
									v-bind:opsdata1="this.opsdata1" 	
									v-bind:opsdata2="this.opsdata2" 
									v-bind:opsdata3="this.opsdata3" 
			/>
			</v-flex>
		</v-layout>

	</v-container>
</template>

<script>

import { db } from "@/db.js";

import DialogOperadorComponent	from "@/components/DialogOperadorComponent";
import DialogInfoExtraComponent from "@/components/DialogInfoExtraComponent";
import TankComponent 			from "@/components/TankComponent";
import CO2Component 			from "@/components/CO2Component";
import DisplayInferiorComponent from "@/components/DisplayInferiorComponent";
import AlarmasComponent 		from "@/components/AlarmasComponent";
import NotificacionesComponent 	from "@/components/NotificacionesComponent";
import FechaComponent 			from "@/components/FechaComponent";
import GraficoLineComponent 	from "@/components/GraficoLineComponent";
import { customConfig } 		from "@/config/custom.config.js";
import moment 					from "moment";
import OpsSummaryComponent 	from "@/components/OpsSummaryComponent";


import RutaComponent2 from "@/components/RutaComponent2";
import TravelRutaComponent from "@/components/TravelRutaComponent";

import miAPI 			from '@/services/api/api.js'

export default {
	components: {
		DialogOperadorComponent,
		DialogInfoExtraComponent,
		TankComponent,
		CO2Component,
		DisplayInferiorComponent,
		AlarmasComponent,
		NotificacionesComponent,
		FechaComponent,
		GraficoLineComponent,
		
		RutaComponent2,
		TravelRutaComponent,
		OpsSummaryComponent
	},

	props: {
		deviceID: String, // Identificador del camión.
		deviceName: String, // Nombre del equipo.
		deviceCoords: String,	//need to pass the current coords of the device: deviceCoords=lat_long
	},

	data() {
		return {
			datosCamion: [],
			deviceUrl: null, 		// Url del dispositivo para pasar a los componentes.
			ultimaLectura: null, 	// Última lectura de los datos desde Firebase (se coge de la base de datos).
			datosAdicionales: [], 	// Lista de datos a mostrar en el diálogo de Información Adicional.
			txtAlarma: null, 		// Texto de las alarmas.
			datosAlarmas:[],
			txtEstado: null, 		// Texto del estado.
			devices_list:[],
			datosCamionDatastore:{},
			deviceCoords_datestamp: null, //need to pass the datastamp for the current coords of the device: deviceCoords=lat_long
			isOnline:false, 

			selectable_vars_for_plot1: ["TANQUE_01__Temperatura","TANQUE_02__Temperatura", "TANQUE_03__Temperatura", "TANQUE_01__Presion", "TANQUE_02__Presion", "TANQUE_03__Presion"],
			show_selectable_vars: false,
			plot_max_points: 100,
			plot_sampling: 5,

			ALLOW_LOGS_LOCAL: false,
			deviceIdActual: null,
			referencia: null, 		// Ref para el on de los watchlist.
			referenciaAlarma: null, // Ref. para el on de las alarmas(texto arriba).
			referenciaEstado: null, // Ref. para el on del estado.
			referenciaUltLect: null, // Ref. para el on de la última lectura.

			itinerary_day:'',
			this_file:"CamionComponent.vue:",
			this_PdVs: [],

			opsdata:{},
			opsdata1: {name:"Descargas", value:"TBD1"},
			opsdata2: {name:"Litros Descargados", value:"TBD2"},
			opsdata3: {name:"Km Recorridos", value:"TBD3"},
			
		};
	},

	watch: {
		deviceID: function() {
			this.montarCamion();
		},
		
		"$store.state.maquinas": function(maquinas) {
			this.devices_list = maquinas;

			console.log(this.this_file+this.devices_list)
			console.log(this.this_file+" unique groups:"+this.device_groups)
			console.log(this.devices_by_group)
			console.log(this.this_file+this.device_customers)	

			//get the info (coming from server in the get request, specific for this truck: filter by name )
			var thismaquina=this.devices_list.filter(obj => {
				return obj.Ind_Device_Name === this.deviceName
				})
			console.log("thismaquina:")
			console.log(thismaquina)
			this.datosCamionDatastore=thismaquina[0]
			console.log(this.datosCamionDatastore)
			
			this.deviceCoords_datestamp=this.datosCamionDatastore.last_pubsub_txt
			console.log("deviceCoords_datestamp:")
			console.log(this.deviceCoords_datestamp)
			
			this.isOnline=this.datosCamionDatastore.online
			console.log("isOnline:")
			console.log(this.isOnline)
		},
	},

	mounted() {
		this.montarCamion();
	},

	beforeDestroy() {
		// Eliminar los listeners del ON.
		this.apagar("fromDestroy");
	},

	methods: {
		apagar(origen) {
			customConfig.ALLOW_LOGS_GLOBAL && this.ALLOW_LOGS_LOCAL && console.log( this.this_file+"%c%s", "color: red; background: #ccc; font-size: 16px;", "¿Apagar camión?" );

			// ----------------------------------------------------------------
			// En Destroy basta con saber si hay un deviceID.
			// En el resto hay que verificar que se cambie de ID.
			// ----------------------------------------------------------------

			if ( (origen == "fromDestroy" && this.deviceIdActual) 
			  || (this.deviceIdActual && this.deviceIdActual != this.deviceID) ) 
			{
				customConfig.ALLOW_LOGS_GLOBAL && this.ALLOW_LOGS_LOCAL && console.log( this.this_file+"%c%s", "color: white; background: blue; font-size: 16px;", "Apagar camión" );

				this.referencia.off("value");
				this.referenciaAlarma.off("value");
				this.referenciaEstado.off("value");
				this.referenciaUltLect.off("value");

				// Limpiar los valores actuales.
				this.deviceIdActual = null;
				this.referencia = null;
				this.referenciaAlarma = null;
				this.referenciaEstado = null;
				this.referenciaUltLect = null;

				customConfig.ALLOW_LOGS_GLOBAL && this.ALLOW_LOGS_LOCAL && console.log( this.this_file+"%c%s", "color: white; background: blue; font-size: 16px;", "ref.OFF !!" );
			}
			// ----------------------------------------------------------------
		},

		montarCamion(){
			console.log(this.this_file+"--in fun: montarCamion")
			// Controlar en hacer el OFF del listener en funcionamiento, si lo hay.
			this.apagar();

			var vueInstance = this;

			this.devices_list = this.$store.getters.getMaquinas;
			//get the info (coming from server in the get request, specific for this truck: filter by name )
			var thismaquina=this.devices_list.filter(obj => {
				return obj.Ind_Device_Name === this.deviceName
				})
			console.log("thismaquina:")
			console.log(thismaquina)
			this.datosCamionDatastore=thismaquina[0]
			console.log(this.datosCamionDatastore)
			this.deviceCoords_datestamp=this.datosCamionDatastore.last_pubsub_txt
			console.log("deviceCoords_datestamp:")
			console.log(this.deviceCoords_datestamp)


			//check prop params
			console.log(this.this_file+"In : Current coords:"+this.deviceCoords)
			// var coords_lat_long = this.deviceCoords.split("_");
			// var current_lat=parseFloat(coords_lat_long[0])
			// var current_long=parseFloat(coords_lat_long[1])

			// Reemplazar . del correo por _
			this.deviceUrl = this.deviceID.replace(".", "_");

			// ----------------------------------------------------------------
			var ref = db.ref("/devices/" + this.deviceUrl + "/_WATCHLIST/op_data/data/");	//willread and save to datosCamion
			ref.on( "value", function(snapshot) 
			{
				console.log("-Reading Watchlist...on...function(snapshot)")
				customConfig.ALLOW_LOGS_GLOBAL && vueInstance.ALLOW_LOGS_LOCAL && console.log( "%c%s", "color: white; background: black; font-size: 16px;", "Camion.on()" );

				var salida = {};
				var adicionales = [];
				const valores = snapshot.val();			//read WATCHES from: db.ref("/devices/" + this.deviceUrl + "/_WATCHLIST/op_data/data/");

				var values = Object.values(valores);

				for (var k in values) 
				{
					// Convertir los campos FECHA al formato estándar y local (excepto para fecha SIEMENS)
					if (values[k]["type"] == "date" && values[k]["name"] != "FECHA Y HORA SIEMENS" )
					{
						salida[values[k]["name"]] = moment.utc(values[k]["value"], "YYYY/MM/DD-HH:mm:ss").local().format( customConfig.FORMATOFECHAHORA );
					}
					// Convertir el campo FECHA  de "FECHA Y HORA SIEMENS" al formato estándar, no cambiar a local.
					else if (values[k]["type"] == "date" && values[k]["name"] == "FECHA Y HORA SIEMENS" )
					{
						salida[values[k]["name"]] = moment.utc(values[k]["value"], "YYYY/MM/DD-HH:mm:ss").format( customConfig.FORMATOFECHAHORA );
					}

					// No añadir el tipo de dato para BOOLEAN, DATE
					else if (values[k]["type"] == "boolean") 
					{
						salida[values[k]["name"]] = values[k]["value"];
					} 
					else 
					{
						// Limitar el número de decimales para ºC y bar.
						if ( customConfig.TIPO_DECIMALES.includes(values[k]["metric_unit"]) ) 
						{
							values[k]["value"] = Number(values[k]["value"]).toFixed( customConfig.NUMERO_DECIMALES );
						}

						salida[values[k]["name"]] = values[k]["value"] + " " + values[k]["metric_unit"];
					}
				}

				// Preparar los datos adicionales.
				adicionales.push({ name: "BLOQ DEVANADERA ON/OFF", 	   	value: salida["BLOQ DEVANADERA ON/OFF"] });
				adicionales.push({ name: "CONEXION BATERIA/ENCHUFADO", 	value: salida["CONEXION BATERIA/ENCHUFADO"] });
				adicionales.push({ name: "MOTOR DEVANADERA ON/OFF", 	value: salida["MOTOR DEVANADERA ON/OFF"] });
				adicionales.push({ name: "NIVEL CO2", 					value: salida["NIVEL CO2"] });
				adicionales.push({ name: "PRES BOMBA", 					value: salida["PRES BOMBA"] });
				adicionales.push({ name: "TEMP DEL COLECTOR",			value: salida["TEMP DEL COLECTOR"] });
				adicionales.push({ name: "TEMP ISOTERMICA",				value: salida["TEMP ISOTERMICA"] });

				// Alimentar el dato de DATA.
				vueInstance.datosCamion = salida;

				vueInstance.datosAdicionales = adicionales;

				// Probar la SETA.
				// vueInstance.datosCamion['SETA DE EMERGENCIA'] = true;

			});
			this.deviceIdActual = this.deviceID;
			this.referencia = ref;

			// ----------------------------------------------------------------
			// Montar el on para la ALARMA.
			var refAlarma = db.ref("/devices/" + this.deviceUrl + "/_MACHINE_Attributes/op_data/data/alarms/value/list");
			refAlarma.on( "value", function(snapshot) 
			{
				console.log("-Reading alarms/list...on...function(snapshot)")

				/* CAMBIAMOS EL FUNCIONAMIENTO INICIAL.
					ANTES: lista de alarmas tipo: alarm001, alarm019, alarm020, alarm021, alarm022
					AHORA: no hay alarmas / hay alarmas.
				*/
				/* ANTES	
				var salida = '';

				const valores = snapshot.val();

				var values = Object.values(valores);

				for (var k in values)
				{
					salida = salida + values[k] + ', ';
				}

				// Eliminar la última coma=  quitar los dos últimos caracteres.
				salida = salida.slice(0, -2);

				// Alimentar el dato de DATA.
				vueInstance.txtAlarma = salida;
				*/
				
				/* CAMBIAMOS EL FUNCIONAMIENTO 23/07/2019 
					Si el texto del primer elemento es No Active alarms. Dejamos la salida ''
					Esto es como un false y no se mostará nada
				*/
				var salida = '';

				const valores = snapshot.val();		//read Alarms from: db.ref("/devices/" + this.deviceUrl + "/_MACHINE_Attributes/op_data/data/alarms/value/list");

				if ( valores[0] != "No Active alarms" )
				{
					salida = 'Alarmas activas'
				}				

				// Alimentar el dato de DATA.
				vueInstance.txtAlarma = salida;
				vueInstance.datosAlarmas = valores;

			});
			this.referenciaAlarma = refAlarma;

			// ----------------------------------------------------------------
			// Montar el on para el ESTADO.
			var refEstado = db.ref("/devices/" + this.deviceUrl + "/_MACHINE_Attributes/op_data/data/status/value");
			refEstado.on( "value", function(snapshot) 
			{
				console.log("-Reading status...on...function(snapshot)")
				// Alimentar el dato de DATA.
				vueInstance.txtEstado = snapshot.val();

			});
			this.referenciaEstado = refEstado;

			// ----------------------------------------------------------------
			// Montar el on para la fecha de última lectura.
			var refUltLect = db.ref("/devices/" + this.deviceUrl + "/_MACHINE_Attributes/op_data/datestamp_data");
			refUltLect.on( "value", function(snapshot) 
			{
				console.log("-Reading datestamp_data...on...function(snapshot)")
				// Alimentar el dato de DATA, cambiando a formato estándar y fecha local.
				vueInstance.ultimaLectura = moment.utc( snapshot.val(), "YYYY/MM/DD-HH:mm:ss").local().format( customConfig.FORMATOFECHAHORA );

			});
			this.referenciaUltLect = refUltLect;

			//load PdV from Firebase
			var refPdV = db.ref("/devices/" + this.deviceUrl + "/PUNTOS_DE_VENTA");
			refPdV.on( "value", function(snapshot) 
			{ 
				console.log("-Reading PUNTOS_DE_VENTA...on...function(snapshot)")
				const valores = snapshot.val();	
				
				var values = Object.values(valores);
				
				console.log("loaded PdV: length: "+values.length)
				console.log(values)

				vueInstance.this_PdVs = values;
			});

			// ----------------------------------------------------------------
			// launch update of charts so that the last 24hrs are shown

			//?ListVar=[DATESTAMP,TANQUE_01__Temperatura,TANQUE_02__Temperatura,TANQUE_03__Temperatura]
			//&begin=2019-11-06 11:01:00
			//&end=2019-11-07 12:24:00
			//&limit=100&sampling=8
			//&plot_number=1&device_name=semace001_m1
			//&comment=

			var lista = [] 
			lista.push("TANQUE_01__Temperatura");
			lista.push("TANQUE_02__Temperatura");
			lista.push("TANQUE_03__Temperatura");
			//var current_datetime= Date.now().utc().format( customConfig.FORMATOFIREBASE );
			//var previous_day=dateObj.setDate(dateObj.getDate()-1);

			var date = new Date()
			date.setDate(date.getUTCDate() - 1);
			date.setHours(0);
			date.setMinutes(0);
			date.setSeconds(0);
			var fechaIni = "";
			// var fechaIni = date.format( customConfig.FORMATOFIREBASE );
			date.setHours(23);
			date.setMinutes(59);
			date.setSeconds(59);			
			var fechaFin = "";
			// var fechaFin = date.format( customConfig.FORMATOFIREBASE );

			//  // Formatos para la conversión local→utc:  FORMATOFIREBASE: "YYYY-MM-DD HH:mm:ss"

			// var fechaIni = moment( this.dateIni + ' ' + this.timeIni + ':00', customConfig.FORMATOFIREBASE ).utc().format( customConfig.FORMATOFIREBASE );
			// var fechaFin = moment( this.dateFin + ' ' + this.timeFin + ':00', customConfig.FORMATOFIREBASE ).utc().format( customConfig.FORMATOFIREBASE );

			var param = '?ListVar=[' 	+ lista.toString() + ']' + 
						'&begin='	 	+ fechaIni + 
						'&end='   	 	+ fechaFin + 
						'&limit=' 	 	+ "100" + 
						'&sampling=' 	+ "5" + 
						'&plot_number=' + "1" + 
						'&device_name=' + this.deviceName + 
						'&comment=' 	+ "daily full day timeseries";
			console.log(this.this_file+"param: "+param)

			// customConfig.ALLOW_LOGS_GLOBAL && this.ALLOW_LOGS_LOCAL && console.log( encodeURI( param ) );

			// // Realizar la petición HTTP.
			// var x = miAPI.sendGrafico( encodeURI( param ) )
			// .then( datos => {
			// 	console.log( 'K01' );
			// 	console.log( 'Retorno=' );
			// 	console.dir( datos );
			// 	console.log( 'MSG=' + datos.msg );
			// 	console.log( 'Message=' + datos.message );
			// 	customConfig.ALLOW_LOGS_GLOBAL && this.ALLOW_LOGS_LOCAL && console.log( 'enviarForm + respuesta de miAPI.sendGrafico' );
			// 	console.log('.then()');

			// 	// En caso correcto la respuesta del backend de II40 es: {"msg":"Thanks for requesting an update to chart 1","result":200}
			// 	if ( datos.msg =='ERROR' )
			// 	{
			// 		// alert('error, vuelva a intentarlo.' );
			// 		this.$store.commit( "showSnackbar", { 'text': 'Se ha producido un error, vuelva a intentarlo.', 'color': 'error'  } );
			// 	}
			// 	else
			// 	{
			// 		this.$store.commit( "showSnackbar", { 'text': 'Se han actualizado los datos correctamente.<br />En unos segundos se actualizará el gráfico.', 'color': 'info'  } );
			// 		// Ocultar el diálogo.
			// 		this.showDialog = false;
			// 	}
			// })
			// .catch( error => console.log('sendGrafico' + error) );

		},

		consultarRuta()
		{
			console.log(this.this_file+"this is ConsultarRuta")
			console.log(this.this_file+"itinerary_day   : " + this.itinerary_day );

			// Transformar las fechas de local a UTC.
			var fechaIni = moment( this.itinerary_day + ' ' + '00:00', customConfig.FORMATOFIREBASE ).utc().format( customConfig.FORMATOFIREBASE );
			var fechaFin = moment( this.itinerary_day + ' ' + '23:59', customConfig.FORMATOFIREBASE ).utc().format( customConfig.FORMATOFIREBASE );

			var param = '?itinerary_day=' 	+ this.itinerary_day + 
						'&begin=' +fechaIni + 
						'&end=' + fechaFin +
						'&device_name=' + this.deviceName ; 
			console.log( this.this_file+param );

			// Realizar la petición HTTP.
			var x = miAPI.consultarRuta( encodeURI( param ) )
			.then( datos => {
				console.log( this.this_file+'Retorno=' );
				console.dir( datos );
				console.log( 'MSG=' + datos.msg );
				console.log( 'Message=' + datos.message );
				console.log('.then()');
				if ( datos.msg =='ERROR' )
				{
					this.$store.commit( "showSnackbar", { 'text': 'Se ha producido un error, vuelva a intentarlo.', 'color': 'error'  } );
				}
				else
				{
					this.$store.commit( "showSnackbar", { 'text': 'Se han actualizado los datos correctamente.<br />En unos segundos se actualizará el la consulta de ruta.', 'color': 'info'  } );
					this.showDialog = false;
				}
			})
			.catch( error => console.log(this.this_file+'ConsultarRuta' + error) );

		},



	}
};
</script>

<style scoped>

.minimo {
	min-width: 800px;
	max-width: 1800px !important;
}

/* ~ Posición para las tuberías ~ 
		LEFT CENTER RIGHT
		┌────┬────┬────┐
		│ TL │ TC │ TR │  TOP
		├────┼────┼────┤
		│ ML │ MC │ MR │  MIDDLE
		├────┼────┼────┤
		│ BL │ BC │ BR │  BOTTOM
		└────┴────┴────┘

		HOR·izontal
		VER·tical

	*/

/* Tuberías para el tanque */
.tuberias_tank {
	background-image: url("../assets/camion/tuberia-ver-fijo.png"), url("../assets/camion/tuberia-ver-fijo.png");
	background-position: 68% top, center bottom;
	background-repeat: no-repeat, no-repeat;
}

.tuberia_hor_degr {
	background-image: url("../assets/camion/tuberia-degradado.png");
	background-position: right bottom;
	background-repeat: no-repeat;
	height: 25px;
}

.tuberia_hor_b {
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: bottom;
	background-repeat: repeat-x;
	height: 25px;
}

.tuberia_hor_t {
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: top;
	background-repeat: repeat-x;
	height: 25px;
}

.tuberia_hor_m {
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: center;
	background-repeat: repeat-x;
}

.tuberia_hor {
	background-image: url("../assets/camion/tuberia.jpg");
}

.tuberia_ver {
	background-image: url("../assets/camion/tuberia_vert.jpg");
}

.tuberia_ver_fijo {
	background-image: url("../assets/camion/tuberia-ver-fijo.png");
}

.tuberia_hor_top {
	height: 25px;
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: top;
	background-repeat: repeat-x;
}

.tuberia_hor_bot {
	height: 25px;
	background-image: url("../assets/camion/tuberia.jpg");
	background-position: bottom;
	background-repeat: repeat-x;
}

.tuberia_vert {
	background-image: url("../assets/camion/tuberia_vert.jpg");
	background-position: 68% center;
	background-repeat: repeat-y;
}

.seta {
	white-space: nowrap;
}

.seta_activa {
	border-radius: 5px;
	color: red;
	background-color: red;
}

.seta_inactiva {
	color: #eee;
}

.blink_me {
	animation: blinker 250ms linear infinite;
}

.blink_me_icon > i {
	animation: blinker_reves 250ms linear infinite;
}

@keyframes blinker {
	50% {
		color: #ffffff;
	}
}

@keyframes blinker_reves {
	50% {
		color: #ff0000;
	}
}


/* Posicionar los textos de última lectura y fecha Siemens, y otros */
.contenedor{
	display: flex;
	flex-wrap: nowrap;
	justify-content: flex-start;
	align-items: baseline;
}

.anchoFijo{
	width: 150px;
}

.offline{
	opacity: 0.5;
}

</style>
