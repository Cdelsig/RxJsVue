<template>
    <div id="weather">
        <div v-for="day in forecast" :key="day.key">
            { day.key }
        </div>
    </div>
</template>

