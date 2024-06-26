<template>
    <div>
        <h2 class="text-indigo-700">Wpisy na bloga</h2>
        <button @click="pobierzWpisy">refresh</button>
        <div v-for="wpis in wpisy">
            <p>{{ wpis }}</p>
        </div>
        <input v-model="nowyBlog" type="text">
        <button @click="dodajWpisy">dodaj</button>
    </div>
</template>

<script>
import { bootcampd2_backend } from 'declarations/bootcampd2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy() {
            await bootcampd2_backend.dodaj_wpis(this.nowyBlog);
        },
        async pobierzWpisy() {
            this.wpisy = await bootcampd2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }

}
</script>