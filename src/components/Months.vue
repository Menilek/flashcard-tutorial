<script setup>
import { ref } from 'vue';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';
import '../assets/carousel.css';

const FrenchMonths = {
    January: "Janvier",
    February: "Février",
    March: "Mars",
    April: "Avril",
    May: "Mai",
    June: "Juin",
    July: "Juillet",
    August: "Aout",
    September: "Septembre",
    October: "Octobre",
    November: "Novembre",
    December: "Décembre",
}

const JanuaryRevealed = ref(false);
const FebruaryRevealed = ref(false);
const MarchRevealed = ref(false);
const AprilRevealed = ref(false);
const MayRevealed = ref(false);
const JuneRevealed = ref(false);
const JulyRevealed = ref(false);
const AugustRevealed = ref(false);
const SeptemberRevealed = ref(false);
const OctoverRevealed = ref(false);
const NovemberRevealed = ref(false);
const DecemberRevealed = ref(false);


const findKey = (obj, value) => {
    return Object.keys(obj).find(key => obj[key] === value);
}

const toggle = (month) => {
    const monthMap = {
        Janvier: () => JanuaryRevealed.value = JanuaryRevealed.value ? false : true,
        Février: () => FebruaryRevealed.value = FebruaryRevealed.value ? false : true,
        Mars: () => MarchRevealed.value = MarchRevealed.value ? false : true,
        Avril: () => AprilRevealed.value = AprilRevealed.value ? false : true,
        Mai: () => MayRevealed.value = MayRevealed.value ? false : true,
        Juin: () => JuneRevealed.value = JuneRevealed.value ? false : true,
        Juillet: () => JulyRevealed.value = JulyRevealed.value ? false : true,
        Aout: () => AugustRevealed.value = AugustRevealed.value ? false : true,
        Septembre: () => SeptemberRevealed.value = SeptemberRevealed.value ? false : true,
        Octobre: () => OctoverRevealed.value = OctoverRevealed.value ? false : true,
        Novembre: () => NovemberRevealed.value = NovemberRevealed.value ? false : true,
        Décembre: () => DecemberRevealed.value = DecemberRevealed.value ? false : true
    }
    monthMap[month]()
}

const isWordRevealed = (month) => {
    const revealMap = {
        Janvier: JanuaryRevealed.value,
        Février: FebruaryRevealed.value,
        Mars: MarchRevealed.value,
        Avril: AprilRevealed.value,
        Mai: MayRevealed.value,
        Juin: JuneRevealed.value,
        Juillet: JulyRevealed.value,
        Aout: AugustRevealed.value,
        Septembre: SeptemberRevealed.value,
        Octobre: OctoverRevealed.value,
        Novembre: NovemberRevealed.value,
        Décembre: DecemberRevealed.value
    }
    return revealMap[month];
}

const monthToShow = (month) => !isWordRevealed(month) ? month : findKey(FrenchMonths, month);
</script>

<template>
    <h2>Months</h2>
    <Carousel :itemsToShow="2" :wrapAround="true">
        <Slide v-for="month in FrenchMonths" :key="month">
            <div class="carousel__item red" @click="toggle(month)">{{ monthToShow(month) }}</div>
        </Slide>
        <template #addons>
            <Navigation />
            <Pagination />
        </template>
    </Carousel>
</template>

<style scoped>

</style>
