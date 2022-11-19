<template>
  <v-dialog v-model="dialog" max-width="500px">
    <form @submit.prevent="submit">
      <v-card>
        <v-card-text>
          <v-card-title> Curso: {{course.name}} </v-card-title>
          <v-text-field v-model="course.name" label="Name" :readonly="true" />
             <v-text-field
          v-model="course.goal"
          label="Goal"
          :readonly="true"
        />
           <v-textarea
          v-model="course.information"
          label="Information"
          :readonly="true"
        />
          <v-textarea
          v-model="course.requirements"
          label="Requirements"
          :readonly="true"
        />
        <v-text-field
          v-model="course.duration"
          label="Duration"
          type="number"
          :readonly="true"
        />
        <v-text-field
          v-model="course.price"
          label="Price"
          :readonly="true"
        />
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog = false"> Fechar </v-btn>
          <v-spacer />
          <v-btn color="success" text @click="goToClasses()"> Ver Turmas </v-btn>
        </v-card-actions>
      </v-card>
    </form>
  </v-dialog>
</template>

<script>
import { useCurrencyInput } from 'vue-currency-input'

export default {
  created() {
    this.$nuxt.$on('viewCourseInfo', ($event) => {
      this.course = $event
      this.dialog = true
    })
  },
  data() {
    return {
      dialog: false,
      course: {},
    }
  },
  methods: {
    goToClasses() {
      this.$router.push({name:'classes', query:{courseId: this.course.id}});
    }
  },
}
</script>

<style>
</style>
