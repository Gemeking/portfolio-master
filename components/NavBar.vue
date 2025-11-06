<template>
  <div>
    <div class="border-right"></div>

    <b-navbar
      toggleable="lg"
      fixed="top"
      :type="themeMode === 'dark' ? 'dark' : 'light'"
      :variant="themeMode === 'dark' ? 'dark' : 'light'"
      class="custom-navbar"
    >
      <!-- Logo -->
      <b-navbar-brand href="/" class="navbar-logo">
        <b-img
          :src="themeMode === 'dark' ? require('@/assets/WHITE.png') : require('@/assets/BLACK.png')"
          alt="Mura Creatives Logo"
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
          <!-- Theme Toggle -->
          <b-nav-item
            href="#"
            @click="toggleDarkMode"
            class="moon-icon"
            title="Toggle Darkmode"
          >
            <SunnyIcon
              v-if="themeMode === 'dark'"
              style="color: #fff; font-size: 26px;"
            />
            <MoonIcon
              v-else
              style="color: #000; font-size: 26px;"
            />
          </b-nav-item>
        </b-navbar-nav>

        <b-navbar-nav class="mx-auto main-nav">
          <b-nav-item to="/">Home</b-nav-item>
          <b-nav-item to="/about">About</b-nav-item>

          <!-- Projects Dropdown -->
          <b-nav-item-dropdown text="Projects" right class="projects-dropdown">
            <b-dropdown-item to="/projects/furniture">Furniture Design</b-dropdown-item>
            <b-dropdown-item to="/projects/graphics">Graphics Design</b-dropdown-item>
            <b-dropdown-item to="/projects/architectural">Architectural</b-dropdown-item>
            <b-dropdown-item to="/projects/interior">Interior</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item to="/contact">Contact Me</b-nav-item>
          <b-nav-item to="/cv">CV</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
require("vue-ionicons/ionicons.css");
import SunnyIcon from "vue-ionicons/dist/md-sunny.vue";
import MoonIcon from "vue-ionicons/dist/md-moon.vue";

export default {
  name: "NavBar",
  components: { SunnyIcon, MoonIcon },
  data() {
    return {
      themeMode: "light",
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
    },
  },
  mounted() {
    if (localStorage.themeMode === "dark") {
      this.themeMode = "dark";
      document.body.classList.add("dark");
    }
  },
};
</script>

<style scoped>
/* Right border decoration */
.border-right {
  position: fixed;
  height: 667px;
  width: 80px;
  right: 0;
  z-index: 1000;
}

/* Navbar Custom Height & Transparent Background */
.custom-navbar {
  height: 100px; /* taller for bigger logo */
  padding: 0 2rem;
  background-color: transparent !important;
  transition: background 0.3s ease;
  z-index: 2000;
  display: flex;
  align-items: center;
}

/* Navbar background on mobile / collapsed menu */
@media (max-width: 991px) {
  .custom-navbar {
    background-color: rgba(0,0,0,0.7) !important;
    backdrop-filter: blur(10px);
  }
}

/* Logo Styling */
.navbar-logo img {
  transition: all 0.3s ease;
  max-height: 200px; /* increase logo size */
  transform: scale(1.2); /* scale up for bigger presence */
}
@media (max-width: 991px) {
  .navbar-logo img {
    max-height: 60px; /* smaller on mobile */
    transform: scale(1); /* normal scale for mobile */
  }
}

/* Nav Styling */
.navbar-nav { margin-left: 0px; }
@media screen and (max-width: 420px) {
  .navbar-nav { margin-left: 0px; }
  .border-right { display:none; }
}

.nav-item { font-size: 16px; margin: 15px; border-radius: 3px; }
.nav-link { color: #000; text-decoration: none; }
body.dark .nav-link { color: #fff; }
.nav-item:hover { background: rgb(243, 240, 240); }
body.dark .nav-item:hover { background: #333; }

/* Theme Toggle */
.moon-icon { cursor: pointer; display: flex; align-items: center; justify-content: center; }
.moon-icon:hover { background: transparent !important; }

/* Thin line between nav items */
.main-nav .nav-item + .nav-item { border-left: 1px solid #dee2e6; padding-left: 15px; }
body.dark .main-nav .nav-item + .nav-item { border-left: 1px solid #444; }

/* Shift main nav slightly left */
.main-nav { transform: translateX(-20px); }
@media (max-width: 991px) { .main-nav { transform: none; } }

/* Projects Dropdown Background (desktop only) */
.projects-dropdown .dropdown-menu {
  background-color: #001f3f;
  border-radius: 5px;
}
.projects-dropdown .dropdown-item { color: #fff !important; }
.projects-dropdown .dropdown-item:hover { background-color: #ff9f43 !important; color: #fff !important; }

/* Ensure mobile dropdown still readable */
@media (max-width: 991px) {
  .projects-dropdown .dropdown-menu {
    background-color: rgba(0,0,0,0.8) !important;
    backdrop-filter: blur(10px);
  }
}
</style>
