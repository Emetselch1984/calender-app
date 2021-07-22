<template>
  <div>
    <h1 class="text-h1">Calender</h1>
    <v-list>
      <v-list-item v-for="event in events" :key="event.id">
        {{ event.name }}
      </v-list-item>
    </v-list>
    <v-btn type="submit" @click="fetchEvents()">fetchEvents</v-btn>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import { mapActions } from "vuex";
export default {
  name: "Calender",
  computed: {
    ...mapGetters("events", ["events"]),
  },
  methods: {
    ...mapActions("events", ["fetchEvents"]),
  },
};
</script>
