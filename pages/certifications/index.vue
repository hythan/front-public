<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="data"
      item-key="name"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Certificados</v-toolbar-title
          ><v-divider class="mx-4" inset vertical></v-divider>
        </v-toolbar>
        <validation-observer ref="search_form">
          <form @submit.prevent="submit" class="card card-md">
            <div class="container__search">
              <validation-provider
                v-slot="validationContext"
                rules="required"
                name="Search"
                tag="div"
              >
                <v-text-field
                  v-model="search"
                  label="Search"
                  placeholder="Digite o CPF do estudante"
                  class="mx-4"
                  :error-messages="validationContext.errors[0]"
                  v-mask="'###.###.###-##'"
                />
              </validation-provider>
              <v-btn type="submit"><v-icon>mdi-magnify</v-icon>Pesquisar</v-btn>
            </div>
          </form></validation-observer
        >
      </template>
      <template v-slot:[`item.actions`]="{ item }" >
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
        { text: 'Student Name', value: 'student.name' },
        { text: 'Course Name', value: 'course.name' },
        { text: 'Actions', value: 'actions' },
      ]
    },
  },
  methods: {
    submit: async function () {
      const isValid = await this.$refs.search_form.validate()

      if (!isValid) {
        return;
      }

      return this.findStudentCertification();
    },
    getOrUpdateCertificationList() {
      if (!this.$auth.loggedIn) {
        return
      }
      this.$axios.get('students/profile').then((response) => {
        this.data = response.data.certifications
      })
    },
    viewCertification(id) {
      this.$nuxt.$emit('generateCertification', id)
    },
    findStudentCertification() {
      this.$axios.get('students/certifications/'+this.search).then((response) => {
        this.data = response.data.certifications
      })
    }
  },
  mounted() {
    this.getOrUpdateCertificationList()
  },

}
</script>
<style scoped>
.container__search {
  display: flex;
  align-items: center;
}
</style>
