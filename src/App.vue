<template>
  <base-card>
        <div class="wraper">
            <h1>Simple Wether App</h1>
        </div>
        <div class="wraper">
            <input id="input" type="text" placeholder="City Name" v-model="input" />
            <button class="btn" @click.prevent="search(input)">Search</button>
        </div>
    </base-card>
    <base-card>
        <base-spinner v-if="isLoading && !invalidInput"></base-spinner>
        <base-dialog v-else-if="!isLoading && invalidInput"></base-dialog>
        <city-name v-else :weatherInfo="weatherInfo"></city-name>
    </base-card>
</template>

<script>
import CityName from './components/pages/CityName.vue';
import axios from 'axios';


export default {
  components: { CityName },
    data() {
        return {
            input: '',
            invalidInput: false,
            isLoading: false,
            weatherInfo: {
                show: false,
                name: ''
            }
        };
    },
    computed: {
        cityPath() {
            return this.weatherInfo.name;
        }
    },
    methods: {
        async search(cityName) {
            if (cityName === '') {
                this.invalidInput = true;
                this.isLoading = false;
                this.weatherInfo.show = false
            } else {
                this.invalidInput = false;
                this.weatherInfo.show = false
                this.isLoading = true;
            }

            axios({
                method: 'get',
                url: `https://api.openweathermap.org/data/2.5/weather?q=${cityName}&appid=09cedd8e05fa817ad86619c9390adb45`
            }).then((res) => {

                const responseData = res;

                this.isLoading = false;

                this.weatherInfo = {
                    show: true,
                    name: responseData.data.name,
                    feelsLike: responseData.data.main.feels_like,
                    humidity: responseData.data.main.humidity,
                    pressure: responseData.data.main.pressure,
                    temp: responseData.data.main.temp,
                    tempMax: responseData.data.main.temp_max,
                    tempMin: responseData.data.main.temp_min,
                    descripion: responseData.data.weather[0].main,
                    icon: responseData.data.weather[0].icon,
                    windSpeed: responseData.data.wind.speed,
                    country: responseData.data.sys.country
                }
            }).catch((err) => {
                this.isLoading = false;
                this.invalidInput = true;
                console.log(err);
            });
        }
    },
    created() {
        this.search('belgrade');
    }
}
</script>

<style>
body {
  background-image: url('https://crawfordcountynow.sagacom.com/files/2021/05/Sunny-Skies-1200x768.jpg');
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  font-family: Copperplate;
}

input[type=text]{
    width:50%;
    border:2px solid #aaa;
    border-radius:4px;
    margin:8px 10px;
    outline:none;
    padding:8px;
    box-sizing:border-box;
    transition:.3s;

}
  
input[type=text]:focus{
    border-color: dodgerBlue;
    box-shadow:0 0 8px 0 dodgerBlue;
}

h1, h2 {
    color: dodgerBlue;
}

.wraper {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
}

.btn {
    font-size: 14px;
    padding: 6px 12px;
    margin-bottom: 0;

    display: inline-block;
    text-decoration: none;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -ms-touch-action: manipulation;
    touch-action: manipulation;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    background-image: none;
    border: 1px solid transparent;
    border-radius: 4px;
    margin-top: 6px;
    height: 40px;
    color: white;
    background-color: dodgerblue;
}
.btn:focus,
.btn:active:focus {
    outline: thin dotted;
    outline: 5px auto -webkit-focus-ring-color;
    outline-offset: -2px;
}
.btn:hover,
.btn:focus {
    border-color: dodgerBlue;
    box-shadow:0 0 8px 0 dodgerBlue;
    text-decoration: none;
}
.btn:active {
    background-image: none;
    outline: 0;
    -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
    box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
}
</style>
