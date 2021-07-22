<template>
  <v-card class="pb-12">
    <v-card-action class="d-flex justify-end pa-2">
      <v-btn icon @click="closeDialog">
        <v-icon size="20px">
          mdi-close
        </v-icon>
      </v-btn>
    </v-card-action>
    <v-card-text>
      <DialogSection icon="mdi-square" :color="event.color || 'blue'">
        {{ event.name }}
      </DialogSection>
    </v-card-text>
  </v-card>
</template>

<script>
import { mapGetters } from "vuex";
import { mapActions } from "vuex";
import DialogSection from "@/components/DialogSection";
export default {
  name: "EventFormDialog",
  components: {DialogSection},
  computed: {
    ...mapGetters("events", ["event"]),
  },
  data: () => ({
    name: '',
  }),
  methods: {
    ...mapActions("events", ["setEvent"]),
    closeDialog(){
      this.setEvent(null)
    }
  },
};
</script>
