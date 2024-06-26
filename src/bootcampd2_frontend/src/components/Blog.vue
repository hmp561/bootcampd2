<template>
    <div>
        <h2 class="text-indigo-700">Wpisy na bloga</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-blue-600 rounded text-white-1000 p-4">refresh</button>
        </div>
        <div class="grid gap-4 mx-6 my-4">
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-2xl bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ wpis }}</p>
            </div>
        </div>
        <div class="flex flex-col justify-center">
            <input v-model="nowyBlog" type="text" class="border-4 border-blue-600 p-4">
            <button @click="dodajWpisy" class="bg-blue-600 rounded text-white-1000 p-4">dodaj</button>
        </div>
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