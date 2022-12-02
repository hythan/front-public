<template>
  <div>
    <v-app-bar fixed app>
      <v-row align="center" justify="center">
        <div class="logo">
          <img class="logo-img" src="~/assets/imgs/logo-maxi.png" />
          Maxiambiental Treinamentos
        </div>
        <v-icon @click.stop="drawer = !drawer"> mdi-menu </v-icon>
      </v-row>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" fixed temporary right>
      <div v-if="isLoggedIn" class="div--loggedin">
        <div class="user-email">{{ this.$auth.state.user.email }}</div>
        <v-btn class="login-logout-btn" @click="handleLogout()">Logout</v-btn>
      </div>
      <v-btn v-else class="login-logout-btn login-btn" @click="handleLogin()"
        >Login</v-btn
      >
      <v-divider />
      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="link-title">{{
              item.title
            }}</v-list-item-title>
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
        {
          title: 'Certifications',
          icon: 'mdi-newspaper-variant-outline',
          to: '/certifications',
        },
      ],
    }
  },
  methods: {
    async handleLogout() {
      await this.$auth.logout()
    },
    handleLogin() {
      this.$router.push('/login')
    },
  },
  computed: {
    isLoggedIn() {
      return this.$auth.loggedIn
    },
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
  color: #b9e85c;
  font-weight: 700;
}
.link-title {
  margin-left: 10px;
}

.login-logout-btn {
  display: flex;
  margin: 15px auto;
}

.login-btn {
  background-color: green !important;
  border: green;
  color: white;
}
.div--loggedin {
  display: flex;
  margin: 15px auto;
  flex-direction: column;
}
.user-email {
  display: flex;
  align-self: center;
}
</style>
