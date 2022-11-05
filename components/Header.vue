<template>
  <div>
    <v-app-bar>
      <v-row align="center" justify="center">
        <div class="logo">
          <img class="logo-img" src="~/assets/imgs/logo-maxi.png" />
          Maxiambiental Treinamentos
        </div>
         <v-icon @click.stop="drawer = !drawer"> mdi-menu </v-icon>
      </v-row>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary right>
      <!-- <v-list-item>
        <v-list-item-avatar>
          <v-img src="https://randomuser.me/api/portraits/men/78.jpg"></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>John Leider</v-list-item-title>
        </v-list-item-content>
      </v-list-item> -->
<!--
      <v-divider></v-divider> -->

      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="link-title">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

      </v-list>
    </v-navigation-drawer>
  </div>
</template>
<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        { title: 'Home', icon: 'mdi-view-dashboard', to: '/' },
        { title: 'Courses', icon: 'mdi-school', to: '/courses' },
      ],
    }
  },
}
</script>
<style scoped>
.logo-img {
  height: 55px;
  width: 80px;
}
.logo {
  margin: 0 auto;
  font-size: 18px;
  color:#b9e85c;
  font-weight: 700;
}
.link-title {
  margin-left: 10px;
}
</style>
