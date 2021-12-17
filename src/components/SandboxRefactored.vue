<template>
    <div class="box">
        <v-btn id="start-btn" v-stream:click="click$" >Start Timer</v-btn>
        <h1>{{ tick$ || '...' }}</h1>
    </div>
</template>

<script>
    import { interval } from 'rxjs';
    import { exhaustMap, map, tap } from 'rxjs/operators';

    export default {
        domStreams: [
            'click$',
        ],
        subscriptions() {
            const tick$ = this.click$.pipe(
                exhaustMap(() => interval(1000)),
                map(i => i++),
                tap(i => console.log(i))
            );

            // subscription block is no longer necessary, but we need to return it
            // also unsubscribes automatically, so destroyed() can go away
            return {
                tick$
            }
        },
    }
    // https://www.youtube.com/watch?v=sgSV681n18I
</script>

<style scoped>
h1 {
    text-align: center;
    padding-top: 50px;
}

.box {
    margin: 10px;
    padding: 10px;
    width: 200px;
    height: 200px;
    border: 3px solid black;
}

</style>