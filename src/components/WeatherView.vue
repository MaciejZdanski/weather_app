<template>
    <div class="weatherView">
        <h1>Weather</h1>

        <div class="cityPicker">
        <input type="text" v-model="cityName">
        <button @click="getLocation">SZUKAJ</button>
        </div>

        <table>
        <tr>
            <th>City</th>
            <td>{{currentCity}}</td>
        </tr>
        <tr>
            <th>LAT</th>
            <td>{{lat}}</td>
        </tr>
        <tr>
            <th>LON</th>
            <td>{{lon}}</td>
        </tr>
        </table>
        
        <div class="currentWeather">
            <table>
                <tr>
                    <th>DATE</th>
                    <td>{{current.dt}}</td>
                </tr>
                <tr>
                    <th>TEMP</th>
                    <td>{{current.temp}}</td>
                </tr>
                <tr>
                    <th>DESC</th>
                    <td>{{current.weather?.[0].description}}</td>
                </tr>
                <tr>
                    <th>ICON</th>
                    <td>{{current.weather?.[0].icon}}</td>
                </tr>
            </table>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'WeatherView',
        data(){
            return{
            cityName: "Katowice",
            lat: "",
            lon: "",
            current: {},
            currentCity: "",
            }
        },
        methods:{
            getWeather(lat, lon){
                console.log("getWeather");
                fetch("https://api.openweathermap.org/data/2.5/onecall?lat="+lat+"&lon="+lon+"&exclude=minutely,hourly,alerts&appid=04677c6a3c533e48a61efafe88c2c5ef")
                .then(dt => dt.json())
                .then(dt => {
                    console.log(dt)
                    this.current = dt.current;
                })
            },
            getLocation(){
                fetch("http://api.openweathermap.org/geo/1.0/direct?q="+this.cityName+"&appid=04677c6a3c533e48a61efafe88c2c5ef")
                .then(dt => dt.json())
                .then(dt => {
                    this.cityName = dt[0].name;
                    this.currentCity = dt[0].name;
                    this.lat = dt[0].lat;
                    this.lon = dt[0].lon;
                    this.getWeather(dt[0].lat, dt[0].lon);
                })
            }
        },
        created(){
            this.getLocation();
        }
    }
</script>

<style>
</style>