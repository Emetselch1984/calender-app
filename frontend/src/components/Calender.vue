<template>
  <div>
    <v-sheet height="6vh" class="d-flex align-center">
      <v-btn outlined small class="ma-4" @click="setToday">今日</v-btn>
      <v-btn icon @click="$refs.calendar.prev()">
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-btn icon icon @click="$refs.calendar.next()">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
    </v-sheet>
    <v-sheet height="94vh">
      <v-calendar
        v-model="value"
        :events="events"
        @change="fetchEvents"
        locale="ja-jp"
        :day-format="(timestamp) => new Date(timestamp.date).getDate()"
        :month-format="
          (timestamp) => new Date(timestamp.date).getMonth() + 1 + ' /'
        "
        @click:event="showEvent"
      ></v-calendar>
    </v-sheet>
    <v-dialog :value="event !== null" @click:outside="closeDialog" width="600">
      <EventDetailDialog v-if="event !== null"/>
    </v-dialog>
  </div>
</template>

<script>
import { format } from "date-fns";
import { mapGetters } from "vuex";
import { mapActions } from "vuex";
import EventDetailDialog from "@/components/EventDetailDialog";
export default {
  name: "Calender",
  components: {EventDetailDialog},
  data: () => ({
    value: format(new Date(), "yyyy/MM/dd"),
    dialogMessage: "",
  }),
  computed: {
    ...mapGetters("events", ["events",'event']),
    title() {
      return format(new Date(this.value), "yyyy年 M月");
    },
  },
  methods: {
    ...mapActions("events", ["fetchEvents",'setEvent']),
    setToday() {
      this.value = format(new Date(), "yyyy/MM/dd");
    },
    showEvent({event}) {
      this.setEvent(event)
    },
    closeDialog(){
      this.setEvent(null)
    }
  },
};
</script>
