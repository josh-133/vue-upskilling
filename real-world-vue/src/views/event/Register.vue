<script setup>
  import { useRouter } from 'vue-router';
  import { inject } from 'vue';
  const { event } = defineProps(["event"])
  const router = useRouter();
  const GStore = inject('GStore');
  const register = () => {
    // If registration API call is successful
    GStore.flashMessage = 'You have successfully registered for ' + event.title;
    setTimeout(() => {
      GStore.flashMessage = '';
    }, 3000);
    router.push({
      name: 'EventDetails'
    });
  }
</script>

<template>
  <div v-if="event">
    <p>Register for the event here.</p>
    <button @click="register">Register Me!</button>
  </div>
</template>
