<script setup lang="ts">
import { ref, onMounted } from 'vue'
import EventService from '../services/EventService'

const props = defineProps({
    id: {
        type: Number,
        required: true,
    },
})

interface Event {
  title: string,
  time: Date,
  date: Date,
  location: string,
  description: string,
}

const event = ref<Event | null>(null)

onMounted(() => {
    EventService.getEvent(props.id)
  .then((response) => {
    event.value = response.data;
    
  })
  .catch((error) => {
    console.log(error);
  })
})
</script>

<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <h1>{{ event.time }} om {{ event.date }} @ {{ event.location }}</h1>
        <h1>{{ event.description }}</h1>
    </div>
</template>