<template>
<form v-on:submit.prevent="getWeather">
    <label>Enter zipcode: </label>
    <input type="text" v-model="zipcode"/>
    <div>
    <input type="submit" value="Get Weather!">
</div>
<div v-if="weatherObj.temperature != ''">
    <p>You are in {{ weatherObj.name }} and today is {{ weatherObj.date }}</p>
    <p>It is {{ weatherObj.temperature }} degrees and it feels like {{ weatherObj.feelsLike }} degrees</p>
    <p>The humidity is {{ weatherObj.humidity }}% out.</p>
    <p>It is {{ weatherObj.description }}</p>
    <img :src="image" alt="">
</div>
</form>

</template>

<script>
import WeatherService from '../services/WeatherService';
export default {
    data(){
        return{
            zipcode: '',
            weatherObj: {},
            image: ''

        }
    },
    methods: {
    getWeather() {
        WeatherService.getWeather(this.zipcode)
        .then((response) => {
            console.log(response);
            this.weatherObj = response.data;
            this.image = "https://openweathermap.org/img/wn/"
            this.weatherObj.icon + ".png";
        })

    }
}
}

</script>

<style scoped>
img {
    width: 100px;
}

</style>