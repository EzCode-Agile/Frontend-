<template>
  <v-card>
    <v-card-title>
      <span class="headline">Edit Diet</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col cols="12" sm="6" md="4">
            <v-text-field v-model="item.id" label="Id"></v-text-field>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-text-field v-model="item.title" label="Title"></v-text-field>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-text-field v-model="item.description" label="Description"></v-text-field>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-text-field v-model="item.user" label="User"></v-text-field>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
      <v-btn color="blue darken-1" text @click="save">Save</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import DietService from "@/services/diets-service";

export default {
  name: "edit-diet",
  data() {
    return {
      item: {
        id: 0,
        username: ''
      }
    }
  },
  methods: {
    retrieveDiet(id) {
      DietService.get(id)
          .then((response) => {
            this.item = response.data;
          })
          .catch(e => {
            console.log((e));
          })
    },

    save() {
      DietService.update(this.item.id, this.item)
          .then(() => {
            this.navigateToDiets();
          })
          .catch(e => {
            console.log(e);
          })
    },
    close() {
      this.navigateToDiets();
    },
    navigateToDiets() {
      this.$router.push({name: 'diets'});
    }
  },
  created() {
    this.retrieveDiet(this.$route.params.id);
  }
}
</script>

<style scoped>

</style>
