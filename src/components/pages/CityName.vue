<template>
    <div>
        <div class="location">
            <font-awesome-icon icon="fa-solid fa-location-dot" class="icon" /> {{ weatherInfo.country }}, {{ weatherInfo.name }}
        </div>
        <div class="three-img">
            <div>
                <div class="img">
                    <div>
                        <img :src="weatherLogo" alt="Weather Icon">
                    </div>
                </div>
                <div class="desc-div">
                    <h1 class="desc">{{ weatherInfo.descripion }}</h1>
                </div>
            </div>
            <div class="info-one">
                <h1 class="temp">Temperature: {{ weatherInfo.temp }}°</h1>
                <div class="min-max">
                    <h2>Max/Min: {{ weatherInfo.tempMax }}°/{{ weatherInfo.tempMin }}°</h2>
                    <h2>Feels Like; {{ weatherInfo.feelsLike }}°</h2>
                    <h2>Humidity: {{ weatherInfo.humidity }}%</h2>
                    <h2>Pressure: {{ weatherInfo.pressure }}hPa</h2>
                    <h2>Wind Speed: {{ weatherInfo.windSpeed }}m/s</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['weatherInfo'],
    computed: {
        weatherLogo() {
            return `http://openweathermap.org/img/wn/${this.weatherInfo.icon}@4x.png`;
        },
    }
}
</script>

<style scoped>
.location {
    background-color: dodgerblue;
    color: white;
    border-radius: 5px;
    padding: 10px;
    width: auto;
    display: inline;
}

.three-img {
    display: flex;
    justify-items: center;
}

.info-one {
    text-align: center;
    margin-top: 10px;
}

.desc-div {
    text-align: center;
}

.desc {
    margin: 0px 40px;
}

.img {
    display: flex;;
}

h2 {
    margin: 0px 40px;
}

h1 {
    margin: 15px 40px;
}
</style>