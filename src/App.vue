<template>
  <div id="app">
    <Headers v-if="isAuthenticated" @logout="handleLogout"/>
    <Sidebar v-if="isAuthenticated" />
    <router-view />
  </div>
  
</template>

<script>
import Login from './components/Login.vue';
import Headers from './components/Headers.vue';
import Sidebar from './components/Sidebar.vue';
import Home from './components/Home.vue';

export default {
  components: {
    Login,
    Headers,
    Sidebar,
    Home
  },

  data() {
    return {
      isAuthenticated: false,
    }
  },
  created (){
    const token = localStorage.getItem('accessToken');
    if (token) {
      this.isAuthenticated = true;
    }
  },
  methods: {
    handleLogout() {
      localStorage.removeItem('accessToekn');
      this.isAuthenticated = false;
      this.$router.push('/');
    }
  }
};
</script>