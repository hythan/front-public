<template>
  <v-dialog v-model="dialog" max-width="500px">
    <form @submit.prevent="submit">
      <v-card>
        <v-card-text>
          <v-card-title> {{ classObj.name }} </v-card-title>
          <v-text-field
            v-model="classObj.name"
            label="Class Name"
            :readonly="true"
          />
          <v-text-field
            v-if="classObj.course"
            v-model="classObj.course.name"
            label="Course Name"
            :readonly="true"
          />
          <v-text-field
            v-model="classObj.information"
            label="Information"
            :readonly="true"
          />
          <v-text-field
            v-model="classObj.location"
            label="Location"
            :readonly="true"
          />
          <v-text-field
            v-model="classObj.classTimes"
            label="Class Time"
            :readonly="true"
          />
          <v-text-field
            v-if="classObj.teacher"
            v-model="classObj.teacher.name"
            label="Teacher"
            :readonly="true"
          />
          <v-menu
            v-model="menu"
            :close-on-content-click="false"
            transition="scale-transition"
            offset-y
            max-width="290px"
            min-width="auto"
            :disabled="true"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="computedDateFormatted"
                label="Start Date"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="classObj.startDate"
              no-title
              @input="menu = false"
              :readonly="true"
            ></v-date-picker>
          </v-menu>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog = false"> Fechar </v-btn>
          <v-spacer />
          <v-btn color="success" text @click="registration()">
            Inscrever-se
          </v-btn>
        </v-card-actions>
      </v-card>
    </form>
  </v-dialog>
</template>

<script>
import Swal from 'sweetalert2'

export default {
  created() {
    this.$nuxt.$on('viewClassInfo', ($event) => {
      this.classObj = $event
      this.dialog = true
    })
  },
  data() {
    return {
      menu: false,
      dialog: false,
      classObj: {},
    }
  },
  methods: {
    async registration() {
      if (!this.$auth.loggedIn) {
        this.$router.push('/login');
        return ;
      }
        this.$axios
          .post('registrations', {
            studentId: this.$auth.$state.user.id,
            classId: this.classObj.id,
          })
          .then((response) => {
            if(response.data.status == 304) {
              Swal.fire('You alredy registrated to this class!', 'Confirm if you alredy payed the registration and verify the start date of this class!', 'error')
              return;
            }
            Swal.fire('Successfuly registrated for this class!', '', 'success')
          })
    },
    formatDate(date) {
      if (!date) return null
      date = date.split('T')
      const [year, month, day] = date[0].split('-')
      return `${day}/${month}/${year}`
    },
  },
  computed: {
    computedDateFormatted() {
      return this.formatDate(this.classObj.startDate)
    },
  },
}
</script>

<style>
</style>
