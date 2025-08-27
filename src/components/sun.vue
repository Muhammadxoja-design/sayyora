<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const sun = ref(null)
const loading = ref(true)
const error = ref(null)
const age = ref('~4.6 Billion Years')

onMounted(async () => {
    try {
        const res = await axios.get('https://api.le-systeme-solaire.net/rest/bodies/soleil')
        sun.value = res.data
        loading.value = false
    } catch (err) {
        error.value = err.message
        loading.value = false
    }
})
</script>

<template>
    <div class="w-screen h-screen bg-black flex items-center justify-center text-white font-sans">
        <div v-if="loading" class="text-4xl font-bold">Loading...</div>
        <div v-else-if="error" class="text-red-500 text-xl">Xatolik: {{ error }}</div>
        <div v-else class="relative w-screen h-screen bg-black overflow-hidden shadow-2xl border border-gray-800">
            <div class="absolute inset-0 bg-cover bg-center opacity-90 hi" </div>
                <div
                    class="absolute top-4 left-3 text-[10px] leading-snug space-y-1 max-w-[160px] md:max-w-[250px] FONT ">
                    <p><b>AGE:</b> {{ age }}</p>
                    <p><b>TYPE:</b> Yellow Dwarf (G2V)</p>
                    <p><b>DIAMETER:</b> {{ (sun.meanRadius * 2).toLocaleString() }} km</p>
                    <p><b>EQUATORIAL G:</b> {{ sun.gravity }} m/s²</p>
                    <p><b>MASS:</b> {{ sun.mass.massValue }} ×10^{{ sun.mass.massExponent }} kg</p>
                    <p><b>CORE TEMP:</b> ~15,000,000 °C</p>
                    <p><b>SURFACE TEMP:</b> ~5,500 °C</p>
                </div>
                <div class="absolute top-4 right-3 text-[10px] leading-snug max-w-[150px] FONT">
                    <h3 class="font-bold">Protective Field</h3>
                    <p>
                        Earth's magnetic field offers some protection from solar storms.
                        However, polar regions are vulnerable as field lines extend vertically downward,
                        allowing solar particles to penetrate.
                    </p>
                </div>
                <div class="absolute bottom-14 left-4 text-[10px] w-[90%] text-gray-200 FONT">
                    <h3 class="font-bold text-white">THE STAR</h3>
                    <p>
                        Our temperamental sun. The image of a massive coronal loop (CME) was captured by NASA's Solar
                        Dynamics Observatory.
                    </p>
                </div>
                <div class="absolute bottom-2 w-full text-center">
                    <h1 class="text-3xl text-yellow-400 tracking-widest font-light text-shadow-amber-300 ">
                        THE SUN
                    </h1>
                </div>
            </div>
        </div>
</template>
<style>
.hi {
    background-image: url("../assets/sun.jpeg");
}

.FONT {
    font-size: 15px;
}

@media only screen and (max-width: 768px) {
    .FONT {
        font-size: 12px;
    }
}

@media only screen and (max-width: 508px) {
    .FONT {
        font-size: 10px;
    }
}
</style>