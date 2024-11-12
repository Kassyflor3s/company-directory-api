<script setup>
import {ref, onMounted, onUnmounted} from 'vue'
import { useRoute } from 'vue-router'
import useAPI from '@/composables/useAPI';
import { faker } from '@faker-js/faker'


const {fetchEmployee, currentEmployee} = useAPI()

onMounted(async () => { 
    await fetchEmployee(route.params.id)
    
})

onUnmounted(() => {
    currentEmployee.value = null
})

const route = useRoute()
</script>

<template>
    <!-- {{route.params.id}} -->
    <main>
        <div v-if="currentEmployee" class="flex flex-col items-center justify-center gap-2">
            <h1 class="text-4xl font-bold p-5">{{ currentEmployee.firstName }} {{ currentEmployee.lastName }}</h1>
            <h1 class="text-2xl p-2">{{ currentEmployee.title }}</h1>
            <h1 class="text-1xl p-2">{{ currentEmployee.userName }} @southtexascollege.edu</h1>
            <h1 class="text-1xl p-2">{{ currentEmployee.quote }}</h1>

            <img class="p-8" :src="faker.image.urlLoremFlickr({category: 'cat'})" />

        </div>
    </main>

</template>