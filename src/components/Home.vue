<template>
	<div class="container">
		<h1>Vista de Hechizos</h1>
		<br><br>
		<div>
			<table class="table centered">
				<thead>
					<tr>
						<th>Nombre</th>
						<th>Dificultad</th>
						<th>Aprendizaje</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="hechizo in hechizos">
						<td>{{hechizo.nombre}}</td>
						<td>{{hechizo.dificultad}}</td>
						<td>{{hechizo.aprendizaje}}</td>
					</tr>
				</tbody>
			</table>
		</div>	
	</div>
</template>

<script>
	import baseUrl from '../../config'
	export default{
		name: 'home',
		data(){
			return{
				hechizo:{
				},
				hechizos: [],
				loading: false
			}
		},
		methods: {
			getHechizos(){
				this.$http.get(`${baseUrl.uri}/hechizos`).then((response)=>{
					this.hechizos=response.body;
				});
			},
			createHechizo(){
				this.loading=true;
				this.$http.post(`${baseUrl.uri}/hechizos/create`,this.hechizo)
				.then((response)=>{
					this.loading=false;
					if(response.body.success){
						swal("Creado con exito!", "Los cambios estan en la tabla", "success");
						this.getHechizos();
					}else{
						sweetAlert("Oops...", "Error al crear", "error");
					}
				});
			},
			modifyHechizo(id){
				this.loading=true;
				this.$http.update(`${baseUrl.uri}/hechizos/update/`+identidad,this.hechizo)
				.then((response)=>{
					this.loading=false;
					if(response.body.success){
						swal("Creado con exito!", "Los cambios estan en la tabla", "success");
						this.getHechizos();
					}else{
						sweetAlert("Oops...", "Error al crear", "error");
					}
				});
			},
			deleteHechizo(id){
					this.loading=true;
					this.$http.delete(`${baseUrl.uri}/hechizos/delete/`+id)
						.then((response)=>{
						this.loading=false;
						if(response.body.success){
							this.getHechizos();
							swal("Deleted!", "Se ha eliminado el Libro", "success");
						}else{
							sweetAlert("Oops...", "Error al crear", "error");
						}
					});
					// });
			}
		},
		beforeMount(){
			this.getHechizos();
		},
		mounted(){
			$('ul.tabs').tabs();
			$('select').material_select();
		}
	}
</script>

<style scoped>
		h2{
			font-family: 'Passion One', cursive;
		}
			#test-swipe-1{
				/*background-color: #E6E2AF;*/
				color: #4C1B1B;
				padding-left: 50px;
				padding-right: 50px;
				padding-top: 20px;
				padding-bottom: 30px;
				text-align: center;
			}
			#test-swipe-2{
				/*background-color: #F6E497;*/
				color: #4C1B1B;
				padding-left: 50px;
				padding-right: 50px;
				padding-top: 20px;
				padding-bottom: 30px;
				text-align: center;
			}
			#test-swipe-3{
				/*background-color: #E6E2AF;*/
				color: #4C1B1B;
				padding-left: 50px;
				padding-right: 50px;
				padding-top: 20px;
				padding-bottom: 30px;
				text-align: center;
			}
			body{
				font-family: 'Libre Franklin', sans-serif;
				font-size: 20px;
			}
		.tabs .indicator {
			background-color: #A7A37E !important;
			color: #4C1B1B !important;
		}
		.tabs {
			background-color: #B9121B !important;
			color: #4C1B1B !important;
			font-family: 'Spectral', serif;
			font-weight: bold;
			border-radius: 30px;
		}
		.tabs .tab a.active {
		  color: white;
		}
		.tabs .tab a:hover {
		  color: gray;
		}
		.tabs .tab a {
		  color: #4C1B1B;
		}
		.table thead{
			font-family: "Times New Roman", Georgia, Serif;
			font-weight: bold;
			font-size: 5px;
		}
		.table{
			font-family: 'Spectral', serif;
			font-size: 17px;
			background: white;
			border-radius:3px;
			border-collapse: collapse;
			height: 320px;
			width: 100%;
			box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
			animation: float 5s infinite;
		}
		#boton{
			background-color: #B8630B;
		}
		th {
		  border-bottom:4px solid;
		  border-right: 1px solid;
		  font-size:23px;
		  font-weight: 100;
		  text-align:left;
		  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
		  vertical-align:middle;
		}
		/* label focus color */
		.input-field input:focus + label {
			color: #4C1B1B !important;
		}
		/* label underline focus color */
		.row .input-field input:focus {
			border-bottom: 1px solid #4C1B1B !important;
			box-shadow: 0 1px 0 0 #4C1B1B !important
		}
		.input-field input:focus + label {
			color: #4C1B1B !important;
		}
		/* label underline focus color */
		.row .input-field input:focus {
			border-bottom: 1px solid #4C1B1B !important;
			box-shadow: 0 1px 0 0 #4C1B1B !important
		}
		.input-field textarea:focus + label {
			color: #4C1B1B !important;
		}
		/* label underline focus color */
		.row .input-field textarea:focus {
			border-bottom: 1px solid #4C1B1B !important;
			box-shadow: 0 1px 0 0 #4C1B1B !important
		}
</style>