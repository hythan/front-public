<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="data"
      item-key="name"
      class="elevation-1"
      :search="search"
      :custom-filter="filterOnlyCapsText"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Certificados</v-toolbar-title
          ><v-divider class="mx-4" inset vertical></v-divider>
        </v-toolbar>
        <v-text-field
          v-model="search"
          label="Search"
          placeholder="Digite o nome do curso"
          class="mx-4"
        />
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              color="blue"
              class="mr-2"
              v-bind="attrs"
              v-on="on"
              @click="viewCertification(item.id)"
            >
              mdi-file-download
            </v-icon>
          </template>
          <span>Baixar Certificado</span>
        </v-tooltip>
      <StudentCertification :certification="item" />
      </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      data: [],
    }
  },
  computed: {
    headers() {
      return [
        { text: 'Student Name', value: 'name' },
        { text: 'Course Name', value: 'course.name' },
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
    getOrUpdateCertificationList() {
       if (!this.$auth.loggedIn) {
          return;
       }
      this.$axios.get('students/profile').then((response) => {
        this.data = response.data.certifications
      })
    },
    viewCertification(id) {
      this.$nuxt.$emit('generateCertification', id);
    }
  },
  mounted() {
    this.getOrUpdateCertificationList()
  },
}
</script>
