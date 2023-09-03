<template>
    <main class="bg-gradient-to-tl from-gray-800 via-gray-600 to-gray-400 w-full min-h-screen grid grid-cols-1">

        <div class="flex justify-center items-center">
            <div v-if="weather == null" class="justify-center rounded-md bg-slate-600 grid grid-cols-6 text-gray-200/60">

                <h4 class="p-4 rounded-lg col-start-2  flex justify-center  col-span-4 text-[25px] font-semibold pt-10">Vue
                    Weather App</h4>

                <div class="p-4 rounded-lg col-start-2 flex justify-center pt-10 col-span-4">
                    <NubesIcon />
                </div>

                <h4 class="p-4 rounded-lg col-start-2 flex justify-center col-span-4 text-[25px] font-semibold pt-4">
                    Encuentra el clima de tu ciudad
                </h4>


                <div class="p-4 rounded-lg col-start-2 flex justify-center col-span-4 text-[25px] font-semibold pt-4 pb-10">

                    <input type="text" name="city" id="city"
                        class="block w-full border-0 py-2 pl-4 pr-20 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6"
                        placeholder="City" v-model="city">
                    <button class="h-full py-2.5 pl-4 pr-5 ring-1 ring-inset ring-slate-800 bg-slate-800 sm:text-sm"
                        @click="findWeather()">
                        Buscar
                    </button>
                </div>
                <h4 class="p-4 rounded-lg col-start-2 flex justify-center col-span-4 text-[15px]" v-if="showError">
                    No se ha encontrado la ciudad
                </h4>
            </div>
            <div v-else class="justify-center rounded-md bg-slate-600 grid grid-cols-6 text-gray-200/60">

                <h4 class="p-4 rounded-lg col-start-2  flex justify-center  col-span-4 text-[25px] font-semibold pt-10">Vue
                    Weather App</h4>


                <div class="col-start-1 col-end-7 flex justify-center">

                    <span class="text-[24px] flex items-end">{{ weather.current.temp_c }}°C </span>
                    <span class="text-[24px] flex items-end">&nbsp;|&nbsp;{{ weather.current.condition.text }}</span>
                    <img :src="weather.current.condition.icon" alt="icon">
                </div>

                <div class="col-start-1 col-end-7 pl-6  pt-10 font-bold text-[34px]">

                    {{ weather.location.name }}, {{ weather.location.country }}
                </div>

                <div class="col-start-1 col-end-7 pl-6 font-semibold">

                    Weather Info
                </div>
                <div class="col-start-1 col-end-7 pl-6 font-semibold pt-4 pb-10">

                    <div class="grid grid-cols-2 gap-4">
                        <div class="...">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-brightness-high" viewBox="0 0 16 16">
                                <path
                                    d="M8 11a3 3 0 1 1 0-6 3 3 0 0 1 0 6zm0 1a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z" />
                            </svg>
                            Índice UV {{ weather.current.uv }}
                        </div>
                        <div class="...">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-droplet" viewBox="0 0 16 16">
                                <path fill-rule="evenodd"
                                    d="M7.21.8C7.69.295 8 0 8 0c.109.363.234.708.371 1.038.812 1.946 2.073 3.35 3.197 4.6C12.878 7.096 14 8.345 14 10a6 6 0 0 1-12 0C2 6.668 5.58 2.517 7.21.8zm.413 1.021A31.25 31.25 0 0 0 5.794 3.99c-.726.95-1.436 2.008-1.96 3.07C3.304 8.133 3 9.138 3 10a5 5 0 0 0 10 0c0-1.201-.796-2.157-2.181-3.7l-.03-.032C9.75 5.11 8.5 3.72 7.623 1.82z" />
                                <path fill-rule="evenodd"
                                    d="M4.553 7.776c.82-1.641 1.717-2.753 2.093-3.13l.708.708c-.29.29-1.128 1.311-1.907 2.87l-.894-.448z" />
                            </svg>
                            Humedad {{ weather.current.humidity }}%
                        </div>
                        <div class="...">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-cloud" viewBox="0 0 16 16">
                                <path
                                    d="M4.406 3.342A5.53 5.53 0 0 1 8 2c2.69 0 4.923 2 5.166 4.579C14.758 6.804 16 8.137 16 9.773 16 11.569 14.502 13 12.687 13H3.781C1.708 13 0 11.366 0 9.318c0-1.763 1.266-3.223 2.942-3.593.143-.863.698-1.723 1.464-2.383zm.653.757c-.757.653-1.153 1.44-1.153 2.056v.448l-.445.049C2.064 6.805 1 7.952 1 9.318 1 10.785 2.23 12 3.781 12h8.906C13.98 12 15 10.988 15 9.773c0-1.216-1.02-2.228-2.313-2.228h-.5v-.5C12.188 4.825 10.328 3 8 3a4.53 4.53 0 0 0-2.941 1.1z" />
                            </svg>
                            Nubosidad {{ weather.current.cloud }}%
                        </div>
                        <div class="...">

                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-wind" viewBox="0 0 16 16">
                                <path
                                    d="M12.5 2A2.5 2.5 0 0 0 10 4.5a.5.5 0 0 1-1 0A3.5 3.5 0 1 1 12.5 8H.5a.5.5 0 0 1 0-1h12a2.5 2.5 0 0 0 0-5zm-7 1a1 1 0 0 0-1 1 .5.5 0 0 1-1 0 2 2 0 1 1 2 2h-5a.5.5 0 0 1 0-1h5a1 1 0 0 0 0-2zM0 9.5A.5.5 0 0 1 .5 9h10.042a3 3 0 1 1-3 3 .5.5 0 0 1 1 0 2 2 0 1 0 2-2H.5a.5.5 0 0 1-.5-.5z" />
                            </svg>{{ weather.current.wind_kph }} Kph {{ weather.current.wind_dir }}
                        </div>
                    </div>
                </div>

            </div>

        </div>

        <!-- ... -->
    </main>
</template>

<script>
import NubesIcon from './NubesIcon.vue'
import { API_KEY, API_URL } from '../config/constants.js'

export default {
    components: {
        NubesIcon
    },
    data() {
        return {
            city: '',
            weather: null,
            showError: false
        }
    },

    methods: {
        getWeather() {

            this.showError = false
            const url_api = `${API_URL}current.json?key=${API_KEY}&q=${this.city}&lang=es`

            return fetch(url_api).then(res => res.json()).then(data => data)
        },
        async findWeather() {
            await this.getWeather().then(data => {

                if (!data.error)
                    this.weather = data
                else
                    this.showError = true
            })
        }

    }
}
</script>