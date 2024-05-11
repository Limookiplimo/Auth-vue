<template>
  <div id="app">
    <Headers v-if="!isLoginPage" @logout="handleLogout" />
    <Sidebar v-if="!isLoginPage" />
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
  computed: {
    isLoginPage() {
      return this.$route.path === '/';
    }
  },
  created() {
    const token = localStorage.getItem('accessToken');
    if (token) {
      this.isAuthenticated = true;
    }
  },
  methods: {
    handleLogout() {
      localStorage.removeItem('accessToken');
      this.isAuthenticated = false;
      this.$router.push('/');
    }
  }
};
</script>