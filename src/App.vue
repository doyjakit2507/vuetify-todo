<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer"
      mobile-breakpoint="768"
      app
    >
      <v-img
        class="pa-4 pt-7"
        src="mountains-1985027_1920.jpg"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar>
          <img src="https://scontent.fbkk12-4.fna.fbcdn.net/v/t1.6435-9/74475383_994966060835999_2234275479534174208_n.jpg?_nc_cat=103&ccb=1-3&_nc_sid=09cbfe&_nc_eui2=AeG1g7VGoY6Rosb_oiNY-tiTdy7t-2OpVfp3Lu37Y6lV-klSZ_cS3zWcyDkeroLuCDsFN-fMYV2Y9vShx8a8MQF_&_nc_ohc=pzLawEbEF64AX-BJ4h0&_nc_ht=scontent.fbkk12-4.fna&oh=2f1313164455085d29681eafe99abd90&oe=60DC55AD" 
          alt="Jakit Ja"
          mb-4>
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Danny Ja
        </div>
        <div class="white--text text-subtitle-1">
          dayny__connell
        </div>
      </v-img>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>

        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="#fcb69f"
      dark
      src="mountains-1985027_1920.jpg"
      prominent
      :height="$route.path ==='/' ? '238' : '170'"
    >
      <template template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-app-bar-title class="text-h4 ml-4">
            <!-- {{ appTitle }} -->
              {{ $store.state.appTitle }}
            </v-app-bar-title>
        </v-row>

        <v-row>
          <live-date-time />
        </v-row>

        <v-row v-if="this.$route.path === '/'">
          <field-add-task />    
        </v-row>

      </v-container>
    </v-app-bar>
    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import LiveDateTime from './components/Tools/LiveDateTime.vue'
  export default {
    data: () => ({ 
      drawer: null ,
      items: [
          { 
            title: 'Dashboard', 
            icon: 'mdi-format-list-checks', 
            to: '/'
          },
          { 
            title: 'About', 
            icon: 'mdi-information-outline', 
            to: '/about'
          },
      ]
    }),
    mounted() {
      console.log(this.$route);
      this.$store.dispatch('getTasks')
    },
    // computed: {
    //   appTitle() {
    //     return process.env.VUE_APP_TITLE
    //   }
    // },
    components: {
      'search': require('@/components/Tools/Search.vue').default,
      'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,
      "field-add-task": require("@/components/Todo/FieldAddTask.vue").default,
      'snackbar': require('@/components/Shared/Snackbar.vue').default
      
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none !important 
</style>