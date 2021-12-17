<template>
    <v-container class="text-center">
        <v-row >
            <v-col cols="12">
                <h1>Hello RxJs!</h1>
            </v-col>
        </v-row>
        <v-row >
            <v-col cols="12" class="mb-10">
                <v-btn @click="getForecastRx()">Click me!</v-btn>
            </v-col>
        </v-row>
        <v-row cols="12" justify="center" >
            <v-col cols="2" v-for="day in forecast" :key="day.key"   >
                <b>{{ new Date(day.date).toLocaleDateString() }}</b>
                <p>{{day.summary.key}}</p>                
                <img :src="day.summary.value" alt="">
            </v-col>
        </v-row>

    </v-container>
</template>

<script>

//import { Observable, Subject, throwError } from 'rxjs';
import { throwError } from 'rxjs';
import { mergeMap, tap, catchError } from 'rxjs/operators';
import { ajax } from 'rxjs/ajax';

export default {
    name: 'HelloRxJs',
    data() {
        return {
            url: "https://localhost:7022/weatherforecast",
            forecast: [],
        }
    },
    methods: {       
        // getImgUrl(pic) {
        //     return `https://openweathermap.org/img/w/${pic}.png`;
        // },       
        getForecastRx() {
            this.forecast = [];
            const obs$ = ajax(this.url)
                .pipe(
                    mergeMap(ajaxResponse => ajaxResponse.response),
                    tap(day => {
                        day.summary.value = `https://openweathermap.org/img/w/${day.summary.value}.png`;
                    }),
                    tap(day => {
                        this.forecast.push(day);
                    }),
                    catchError((err) => {
                        return throwError(() => err)
                    })
                )
            obs$.subscribe();
        },
        async getForecastFetch() {
            const response = await fetch(this.url);
            if (response.ok === true) {
                const data = await response.json();
                data.map(day => {
                    day.summary.value = `https://openweathermap.org/img/w/${day.summary.value}.png`;
                    this.forecast.push(day);
                });
            }
        }
    }
}
</script>

