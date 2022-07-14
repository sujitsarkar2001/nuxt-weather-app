<template>
    <v-container>
        <v-layout class="mt-3">
            <v-row>

                <v-col cols="12">
                    <h2 class="display-1 text-center">Weather App</h2>
                </v-col>

                <v-col cols="12">
                    <v-card class="blue-grey darken-2">
                        <v-card-text class="white--text">
                            <v-layout justify-center>
                                <v-flex class="text-center">
                                    <h4>Temperature</h4>
                                    <h1 class="display-1">{{ weather.name }}</h1>
                                    <img :src="icon" :alt="weather.name">
                                    <p>
                                        <span class="display-1">{{ weather.name }}</span>
                                        <span class="caption mt-4">{{ weather.weather[0].description }}</span>
                                    </p>
                                </v-flex>
                            </v-layout>
                        </v-card-text>
                    </v-card>
                </v-col>

                <v-col cols="12">
                    <v-form @submit.prevent="search">
                        <v-text-field
                            label="Enter city name"
                            v-model="city"
                        ></v-text-field>
                    </v-form>
                </v-col>

            </v-row>
        </v-layout>
    </v-container>
</template>

<script>
export default {
    head() {
        return {
            title: 'Weather App'
        }
    },
    data() {
        return {
            weather: {},
            city: 'Sylhet'
        }
    },
    asyncData({ params, $axios }) {
        return $axios.$get(`https://api.openweathermap.org/data/2.5/weather?q=Sylhet&appid=cc796b86e6a1cd99df8e49c57149d7b3`)
                    .then(response => {
                        return { weather: response }
                    })
    },
    computed: {
        icon() {
            return this.weather.weather ? `https://openweathermap.org/img/w/${this.weather.weather[0].icon}.png` : ''
        }
    },
    created () {
        this.getWeatherInfo()
    },
    methods: {
        getWeatherInfo() {
            this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${process.env.WEATHER_APP_ID}`)
                    .then(response => {
                        console.log(response);
                        this.weather = response
                    })
        },
        search() {
            this.getWeatherInfo()
        },
    }
}
</script>