<template>
  <v-card class="pb-12">
    <v-card-action class="d-flex justify-end pa-2">
      <v-btn icon @click="closeDialog">
        <v-icon size="20px">
          mdi-close
        </v-icon>
      </v-btn>
    </v-card-action>
    <v-card-title>
      <DialogSection icon="mdi-square" :color="event.color || 'blue'">
        {{ event.name }}
      </DialogSection>
    </v-card-title>
    <v-card-text>
      <DialogSection icon="mdi-clock-time-three-outline">
        {{ event.start.toLocaleString() }} ~~ {{ event.end.toLocaleString() }}
      </DialogSection>
    </v-card-text>
    <v-card-text>
      <DialogSection icon="mdi-card-text-outline">
        {{ event.description  || 'no description'}}
      </DialogSection>
    </v-card-text>
  </v-card>
</template>

<script>
import { mapGetters } from "vuex";
import { mapActions } from "vuex";
import DialogSection from "@/components/DialogSection";
export default {
  name: "EventDetailDialog",
  components: {DialogSection},
  data: () => ({
    value: format(new Date(), "yyyy/MM/dd"),
    dialogMessage: "",
  }),
  computed: {
    ...mapGetters("events", ['event']),
  },
  methods: {
    ...mapActions("events", ['setEvent']),
    closeDialog(){
      this.setEvent(null)
    }
  },
};
</script>
