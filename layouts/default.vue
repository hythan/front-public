<template>
  <v-app dark>
    <Header />
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} todos os direitos reservados.</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-shield-crown',
          title: 'Admins',
          to: '/admins',
        },
        {
          icon: 'mdi-account-school',
          title: 'Students',
          to: '/students',
        },
        {
          icon: 'mdi-account-tie',
          title: 'Teachers',
          to: '/teachers',
        },
        {
          icon: 'mdi-school',
          title: 'Courses',
          to: '/courses',
        },
        {
          icon: 'mdi-account-group',
          title: 'Classes',
          to: '/classes',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Maxiambiental Admin',
    }
  },
}
</script>
<style scoped>
.username-logedin-mobile {
  display: block;
  font-size: 14px;
  margin: 5px 15px;
  text-transform: uppercase;
  border-bottom: 1px solid grey;
}
.list-liks,
.container-logout-btn {
  height: 50%;
}

.container-logout-btn {
  display: flex;
  align-items: flex-end;
}

.logout-btn-mobile {
  width: 100%;
}

.username-logedin-desktop,
.logout-btn-desktop {
  display: none;
}

@media screen and (min-width: 1024px) {
  .username-logedin-mobile,
  .logout-btn-mobile {
    display: none;
  }
  .container-logout-btn {
    height: 0;
  }
  .username-logedin-desktop {
    display: block;
    text-transform: uppercase;
  }

  .logout-btn-desktop {
    display: block;
    margin: 0 20px;
  }
}
</style>
