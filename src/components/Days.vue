<script setup>
import { ref } from 'vue';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';
import '../assets/carousel.css';

const FrenchDays = {
    Monday: "Lundi",
    Tuesday: "Mardi",
    Wednesday: "Mercredi",
    Thursday: "Jeudi",
    Friday: "Vendredi",
    Saturday: "Samedi",
    Sunday: "Dimanche"
}

const MondayRevealed = ref(false);
const TuesdayRevealed = ref(false);
const WednesdayRevealed = ref(false);
const ThursdayRevealed = ref(false);
const FridayRevealed = ref(false);
const SaturdayRevealed = ref(false);
const SundayRevealed = ref(false);

const findKey = (obj, value) => {
    return Object.keys(obj).find(key => obj[key] === value);
}

const toggle = (day) => {
    const dayMap = {
        Lundi: () => MondayRevealed.value = MondayRevealed.value ? false : true,
        Mardi: () => TuesdayRevealed.value = TuesdayRevealed.value ? false : true,
        Mercredi: () => WednesdayRevealed.value = WednesdayRevealed.value ? false : true,
        Jeudi: () => ThursdayRevealed.value = ThursdayRevealed.value ? false : true,
        Vendredi: () => FridayRevealed.value = FridayRevealed.value ? false : true,
        Samedi: () => SaturdayRevealed.value = SaturdayRevealed.value ? false : true,
        Dimanche: () => SundayRevealed.value = SundayRevealed.value ? false : true
    }
    dayMap[day]()
}

const isWordRevealed = (day) => {
    const revealMap = {
        Lundi: MondayRevealed.value,
        Mardi: TuesdayRevealed.value,
        Mercredi: WednesdayRevealed.value,
        Jeudi: ThursdayRevealed.value,
        Vendredi: FridayRevealed.value,
        Samedi: SaturdayRevealed.value,
        Dimanche: SundayRevealed.value
    }
    return revealMap[day];
}

const dayToShow = (day) => !isWordRevealed(day) ? day : findKey(FrenchDays, day);
</script>

<template>
    <h2>Days</h2>
    <Carousel :itemsToShow="2" :wrapAround="true">
        <Slide v-for="day in FrenchDays" :key="day">
            <div class="carousel__item red" @click="toggle(day)">{{ dayToShow(day) }}</div>
        </Slide>
        <template #addons>
            <Navigation />
            <Pagination />
        </template>
    </Carousel>
</template>

<style scoped>

</style>
