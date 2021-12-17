<template>
    <div class="box">
        <v-btn id="start-btn">Start Timer</v-btn>
        <h1>{{ time }}</h1>
    </div>
</template>

<script>
    import { interval, fromEvent } from 'rxjs';
    import { exhaustMap, map, tap } from 'rxjs/operators';

    export default {
        data: () => ({
            time: '...',
            subscription: null,
        }),
        mounted() {
            const buttonElement = document.querySelector('#start-btn');
            const click$ = fromEvent(buttonElement, 'click');
            const tick$ = click$.pipe(
                //exhaustMap(() => interval(1000)).pipe(take(5)),
                exhaustMap(() => interval(1000)),
                map(i => i++),
                tap(i => console.log(i))
            );
            this.subscription = tick$.subscribe(i => {
                this.time = i
            });
        },
        destroyed() {
            this.subscription.unsubscribe();
        }
    }

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