<template>
  <b-navbar
    toggleable="lg"
    fixed="top"
    :type="themeMode === 'dark' ? 'dark' : 'light'"
    :variant="themeMode === 'dark' ? 'dark' : 'light'"
  >
    <!-- Brand Logo -->
    <b-navbar-brand tag="h1" to="/" style="font-weight: bolder;">
      <img
        src="@/assets/mura-creatives-logo.png"
        alt="Mura Creatives Logo"
        class="brand-logo"
      />
    </b-navbar-brand>

    <!-- Navbar Toggle for Mobile -->
    <b-navbar-toggle target="nav-collapse" style="border-radius: 0;" />

    <!-- Collapsible Menu -->
    <b-collapse
      id="nav-collapse"
      is-nav
      class="animate__animated animate__fadeInDown"
    >
      <b-navbar-nav>
        <b-nav-item to="/">Home</b-nav-item>
        <b-nav-item to="/about">About</b-nav-item>
        <b-nav-item to="/projects">Projects</b-nav-item>
        <b-nav-item to="/articles">Articles</b-nav-item>
        <b-nav-item to="/contact">Contact Me</b-nav-item>

        <!-- Theme Toggle -->
        <b-nav-item
          href="#"
          @click="toggleDarkMode"
          class="moon-icon"
          title="Toggle Darkmode"
        >
          <SunnyIcon
            v-if="themeMode === 'dark'"
            style="color: #fff; font-size: 22px;"
          />
          <MoonIcon
            v-else
            style="color: #000; font-size: 22px;"
          />
        </b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
require("vue-ionicons/ionicons.css");
import SunnyIcon from "vue-ionicons/dist/md-sunny.vue";
import MoonIcon from "vue-ionicons/dist/md-moon.vue";

export default {
  name: "NavBar",
  components: {
    SunnyIcon,
    MoonIcon
  },
  data() {
    return {
      themeMode: "light"
    };
  },
  methods: {
    toggleDarkMode() {
      if (this.themeMode === "light") {
        this.themeMode = "dark";
        localStorage.themeMode = "dark";
        document.body.classList.add("dark");
      } else {
        this.themeMode = "light";
        localStorage.themeMode = "light";
        document.body.classList.remove("dark");
      }
    }
  },
  mounted() {
    // Load saved theme
    if (localStorage.themeMode === "dark") {
      this.themeMode = "dark";
      document.body.classList.add("dark");
    }
  }
};
</script>

<style scoped>
/* Logo Styling */
.brand-logo {
  height: 40px;
  width: auto;
  padding: 6px;
  background: #000; /* black background */
  border-radius: 6px;
  box-shadow: 0 0 12px rgba(0, 0, 0, 0.8);
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

.brand-logo:hover {
  transform: scale(1.05);
  box-shadow: 0 0 20px rgba(0, 0, 0, 1);
}

/* Nav Styling */
.navbar-nav {
  margin-left: 100px;
}
@media screen and (max-width: 420px) {
  .navbar-nav {
    margin-left: 0px;
  }
}
.nav-item {
  font-size: 14px;
  margin: 15px;
  border-radius: 2px;
}
.nav-link a {
  color: #000 !important;
  text-decoration: none;
}
.nav-item:hover {
  background: rgb(243, 240, 240);
}

/* Theme Toggle */
.moon-icon {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}
.moon-icon:hover {
  background: transparent !important;
}
</style>
