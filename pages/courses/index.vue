<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="courses"
      item-key="name"
      class="elevation-1"
      :search="search"
      :custom-filter="filterOnlyCapsText"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Cursos</v-toolbar-title
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
              @click="viewCourseInfo(item)"
            >
              mdi-eye
            </v-icon>
          </template>
          <span>Informações</span>
        </v-tooltip>
      </template>
    </v-data-table>
    <CourseInfo />
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      courses: [],
    }
  },
  computed: {
    headers() {
      return [
        { text: 'Name', value: 'name' },
        { text: 'Price', value: 'price' },
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
    getOrUpdateCoursesList() {
      this.$axios.get('courses').then((response) => {
        this.courses = response.data
        this.courses.forEach((e) => {
          e.price = (new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(Number(e.price/100)))
        })
      })
    },
    viewCourseInfo(course) {
      this.$nuxt.$emit('viewCourseInfo', course);
    }
  },
  mounted() {
    this.getOrUpdateCoursesList()
  },
}
</script>
