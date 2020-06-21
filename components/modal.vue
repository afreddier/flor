<template>
    <v-dialog v-model="dialog" persistent max-width="290">
      <v-card>
        <v-card-title class="headline">{{ alertError.title }}</v-card-title>
        <v-card-text>{{ alertError.description }}</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dialog = false" v-if="alertError.buttonClose">{{ alertError.buttonClose }}</v-btn>
          <v-btn color="green darken-1" text @click="dialog = false" v-if="alertError.buttonAccept">{{ alertError.buttonAccept }}</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
  export default {
    props: {
      alertError: {
        type: Object
      }
    },
    data () {
      return {
        dialog: false
      }
    },
    watch: {
      alertError: function (val, oldval) {
        this.dialog = val.dialog;
      }
    }
  }
</script>