<template>
  <div>
    <h1>Calender</h1>
    <ul>
      <li v-for="event in events" :key="event.id">
        {{ event.name }}
      </li>
    </ul>
    <button type="submit" @click="fetchEvents">fetchEvents</button>
    <CalenderDetails />
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import { mapActions } from "vuex";
import CalenderDetails from "@/components/CalenderDetails";
export default {
  name: "Calender",
  components: { CalenderDetails },
  computed: {
    ...mapGetters("events", ["events"]),
  },
  methods: {
    ...mapActions("events", ["fetchEvents"]),
  },
};
</script>
