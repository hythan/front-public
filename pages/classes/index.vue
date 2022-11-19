<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="classes"
      item-key="name"
      class="elevation-1"
      :search="search"
      :custom-filter="filterOnlyCapsText"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Turmas Abertas</v-toolbar-title
          ><v-divider class="mx-4" inset vertical></v-divider>
        </v-toolbar>
        <v-text-field v-model="search" label="Search" class="mx-4" />
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              color="blue"
              small
              class="mr-2"
              v-bind="attrs"
              v-on="on"
              @click="viewClassInfo(item)"
            >
              mdi-eye
            </v-icon>
          </template>
          <span>Informações</span>
        </v-tooltip>
         <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              color="green"
              small
              class="mr-2"
              v-bind="attrs"
              v-on="on"
              @click="registration(item)"
            >
              mdi-note-edit-outline
            </v-icon>
          </template>
          <span>Inscrever-se</span>
        </v-tooltip>
      </template>
    </v-data-table>
    <ClassInfo />
  </div>
</template>

<script>
import Swal from 'sweetalert2'

export default {
  data() {
    return {
      search: '',
      classes: [],
    }
  },
  computed: {
    headers() {
      return [
        { text: 'Name', value: 'name' },
        { text: 'Actions', value: 'actions' },
      ]
    },
  },
  methods: {
    filterOnlyCapsText(value, search, item) {
      return (
        value != null &&
        search != null &&
        typeof value === 'string' &&
        value.toString().toLocaleLowerCase().indexOf(search) !== -1
      )
    },
    getOrUpdateClassesList() {
      this.$axios.get('classes', {
         params: this.$route.query,
      }).then((response) => {
        this.classes = response.data
        this.classes = this.classes.filter(
          (item) => (new Date(item.startDate).getTime()) >= ((new Date()).getTime())
      )
    })
    },
    viewClassInfo(classObj) {
      this.$nuxt.$emit('viewClassInfo', classObj);
    },
     async registration(classObj) {
      if (!this.$auth.loggedIn) {
        this.$router.push('/login');
        return ;
      }
        this.$axios
          .post('registrations', {
            studentId: this.$auth.$state.user.id,
            classId: classObj.id,
          })
          .then((response) => {
            if(response.data.status == 304) {
              Swal.fire('You alredy registrated to this class!', 'Confirm if you alredy payed the registration and verify the start date of this class!', 'error')
              return;
            }
            Swal.fire('Successfuly registrated for this class!', '', 'success')
          })
    },
  },
  mounted() {
    this.getOrUpdateClassesList()
  },
}
</script>
