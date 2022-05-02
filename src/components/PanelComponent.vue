<template>
	<div class="glass">
			<div>

				<transition name="load">

					<div class="error" v-if="error">
						<span><strong>Oh no, make sure you did your search properly.</strong></span>
					</div>

				</transition>


				<transition name="load">

					<div class="output" v-show="loaded">
						<div class="name">
							<h1>{{weather.location}}</h1>
							<span>{{weather.main}}</span>
						</div>

						<div class="numbers">
							<h1>{{weather.temp}} °C</h1>
							<span>{{weather.wind}} / {{weather.humidity}}</span>
						</div>
					</div>

				</transition>

				<div class="inputs">
					<input type="Text" v-model="city" placeholder="City, Two‑letter Abbreviation">
					<button @click="getWeather">Search</button>
				</div>

			</div>
	</div>
</template>

<script>
export default {
	data(){
		return {
			city: '',
			weather: {
				temp: 0,
				location: '',
				main: '',
				wind: '',
				humidity: ''
			},
			loaded: false,
			error: false
		};
	},
	methods:{
		getWeather(){

			this.error = false;

			//url para buscar la ciudad
			const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=1a04d54de8892d3f9f32df0ed32e6c25&units=metric`;

			//se hace la peticion a la API
			fetch(url)
			.then(response => {

				if(response.ok){
					return response.json();
				}else{
					this.error = true
				}

			})
			.then(data => {

				// se asignan los datos recibidos a sus variables correspondientes
				this.weather.location = data.name + ', ' + data.sys.country 
				this.weather.temp = data.main.temp
				this.weather.main = data.weather[0].description
				this.weather.humidity = 'Humidity: ' + data.main.humidity + '%'
				this.weather.wind = 'Wind: ' + data.wind.speed

				// se muestra en pantalla los resultados
				this.loaded = true
			})
		}
	}
}
</script>

<style scoped>
.name {
	text-align: center	;
}

.name h1{
	margin-bottom: 0px;
}

.numbers h1 {
	margin-bottom: 0px;
	margin: 0px;
}

.numbers{
	margin-top: 1em;
	background-color: white;
	padding: 0.5em;
	border-radius: 10px;
	text-align: center;
}

.error {
	width: auto;
	text-align: center;
	background: rgb(214,0,22);
	background: linear-gradient(0deg, rgba(214,0,22,1) 0%, rgba(255,91,97,1) 62%, rgba(255,0,52,1) 100%); 
	border-radius: 10px;
	padding: 0.2em;
	color: white;
	margin-bottom: 10px;
}

h1 {
	text-align: center;
}

button {
	font-size: 15px;
	padding: 0.5em;
	border-radius: 10px 10px 0px 0px;
	border: 1px solid rgba(80, 150, 250, 1.0);
	background: rgb(0,177,214);
	background: linear-gradient(0deg, rgba(0,177,214,1) 0%, rgba(91,207,255,1) 62%, rgba(0,212,255,1) 100%); 
	color:  white;
	width: 100%;
	margin-top: 10px;
}

.output{
	background-color: rgba(300, 300, 300, 0.6);
	border-radius: 10px;
	padding: 1em;
	margin-bottom: 1em;
}

.inputs input{
	width: 96%;
	font-size: 16px;
	border-radius: 10px;
	border: 0px solid grey;
	padding: 5px;
	box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.50);
}

.inputs{
	background-color: rgba(300, 300, 300, 0.6);
	border-radius: 10px;
	padding: 1em 1em 0em 1em;
	text-align: center;
	display: flex;
	flex-direction: column;
}

.glass{
	width: 280px;
	box-shadow: 0 0 1rem rgba(0, 0, 0, 0.4);
	padding: 1em;
	position: relative;
	border-radius: 10px;
	background: inherit;
	color: black;
	z-index: 1;
}

.glass:before{
	content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
	box-shadow: inset 0 0 2000px rgba(200, 200, 200, .5);
    filter: blur(5px);
    background: inherit;
    z-index: -1;
}


.load-enter-from,
.load-leave-to {
	opacity: 0;
}

.load-enter-active,
.load-leave-active {
	transition: 0.3s;
}

.load-enter-to,
.load-leave-from {
	opacity: 1;
}
</style>