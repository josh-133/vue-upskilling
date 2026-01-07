<script setup>
  import EventService from '@/services/EventService';
  import { onMounted, ref, computed } from 'vue';

  const props = defineProps(["id"])
  const event = ref("")
  const id = computed(() => props.id);

  onMounted(() => {
    EventService.getEvent(id.value)
        .then(response => {
          event.value = response.data;
        })
        .catch(error => {
          console.error('Error fetching events:', error);
        });
  })
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails'}">
        Details
      </router-link>
      |
      <router-link :to="{ name: 'EventRegister'}">
        Register
      </router-link>
      |
      <router-link :to="{ name: 'EventEdit'}">
        Edit
      </router-link>
    </div>
    <router-view :event="event"></router-view>
  </div>
</template>
