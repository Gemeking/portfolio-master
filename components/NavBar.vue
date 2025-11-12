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
          class="logo-img"
        />
      </b-navbar-brand>

      <!-- Navbar Toggle for Mobile -->
      <b-navbar-toggle target="nav-collapse" class="custom-toggle">
        <span class="navbar-toggler-icon"></span>
      </b-navbar-toggle>

      <!-- Collapsible Menu -->
      <b-collapse
        id="nav-collapse"
        is-nav
        class="navbar-collapse animate__animated animate__fadeInDown"
      >
        <!-- Theme Toggle -->
        <b-nav-item
          href="#"
          @click="toggleDarkMode"
          class="theme-toggle"
          title="Toggle Darkmode"
        >
          <SunnyIcon
            v-if="themeMode === 'dark'"
            class="theme-icon"
          />
          <MoonIcon
            v-else
            class="theme-icon"
          />
        </b-nav-item>

        <!-- Main Navigation -->
        <b-navbar-nav class="main-nav">
  <b-nav-item to="/" class="nav-link-item" @click="closeNav">Home</b-nav-item>
  <b-nav-item to="/about" class="nav-link-item" @click="closeNav">About</b-nav-item>

  <!-- Projects Dropdown -->
  <b-nav-item-dropdown 
    text="Projects" 
    right 
    class="projects-dropdown nav-link-item"
  >
    <b-dropdown-item to="/projects/furniture" class="dropdown-item-custom" @click="closeNav">Furniture Design</b-dropdown-item>
    <b-dropdown-item to="/projects/graphics" class="dropdown-item-custom" @click="closeNav">Graphics Design</b-dropdown-item>
    <b-dropdown-item to="/projects/architectural" class="dropdown-item-custom" @click="closeNav">Architectural</b-dropdown-item>
    <b-dropdown-item to="/projects/interior" class="dropdown-item-custom" @click="closeNav">Interior</b-dropdown-item>
  </b-nav-item-dropdown>

  <b-nav-item to="/contact" class="nav-link-item" @click="closeNav">Contact Me</b-nav-item>
  <b-nav-item to="/cv" class="nav-link-item" @click="closeNav">CV</b-nav-item>
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
  closeNav() {
    // Collapse the navbar on mobile
    this.$root.$emit('bv::toggle::collapse', 'nav-collapse');
  }
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
/* THEME VARIABLES */
:root { 
  --navbar-bg-light: rgba(255, 255, 255, 0.95);
  --navbar-bg-dark: rgba(0, 31, 63, 0.95); 
  --text-light: #111111; 
  --text-dark: #ffffff; 
  --accent-light: #001f3f;
  --accent-dark: #ff9f43; 
  --hover-light: rgba(0, 31, 63, 0.1); 
  --hover-dark: rgba(255, 255, 255, 0.1); 
  --border-light: rgba(0, 0, 0, 0.1); 
  --border-dark: rgba(255, 255, 255, 0.1); 
  --dropdown-bg-light: #ffffff; 
  --dropdown-bg-dark: #001f3f; 
}

/* Right border decoration */
.border-right {
  position: fixed;
  height: 667px;
  width: 80px;
  right: 0;
  z-index: 1000;
  background: linear-gradient(to right, transparent, var(--accent-light));
}

body.dark .border-right {
  background: linear-gradient(to right, transparent, var(--accent-dark));
}

/* Navbar Custom Height & Background */
.custom-navbar {
  height: 100px;
  padding: 0 2rem;
  background-color: var(--navbar-bg-light) !important;
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  z-index: 2000;
  display: flex;
  align-items: center;
}

body.dark .custom-navbar {
  background-color: var(--navbar-bg-dark) !important;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.3);
}

/* Logo Styling */
.navbar-logo {
  margin-right: auto;
}

.logo-img {
  height: 200px;
  width: 160%;
  transition: all 0.3s ease;
  filter: brightness(1);
}

/* Custom Toggle Button */
.custom-toggle {
  border: none;
  padding: 8px;
  border-radius: 4px;
  background: transparent;
}

.custom-toggle:focus {
  outline: none;
  box-shadow: none;
}

.custom-toggle .navbar-toggler-icon {
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' width='30' height='30' viewBox='0 0 30 30'%3e%3cpath stroke='rgba(0, 31, 63, 0.8)' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
}

body.dark .custom-toggle .navbar-toggler-icon {
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' width='30' height='30' viewBox='0 0 30 30'%3e%3cpath stroke='rgba(255, 255, 255, 0.8)' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
}

/* Navbar Collapse */
.navbar-collapse {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  flex-grow: 0;
}

/* Theme Toggle */
.theme-toggle {
  margin-right: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  transition: all 0.3s ease;
  cursor: pointer;
}

.theme-toggle:hover {
  background-color: var(--hover-light);
}

body.dark .theme-toggle:hover {
  background-color: var(--hover-dark);
}

.theme-icon {
  font-size: 22px;
  color: var(--accent-light);
  transition: all 0.3s ease;
}

body.dark .theme-icon {
  color: var(--accent-dark);
}

/* Main Navigation */
.main-nav {
  display: flex;
  align-items: center;
  gap: 0;
}

.nav-link-item {
  margin: 0;
  padding: 0 1rem;
  position: relative;
}

.nav-link-item .nav-link {
  color: var(--text-light);
  font-weight: 500;
  font-size: 16px;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  transition: all 0.3s ease;
  position: relative;
  text-decoration: none;
}

body.dark .nav-link-item .nav-link {
  color: var(--text-dark);
}

.nav-link-item .nav-link:hover {
  color: var(--accent-light);
  background-color: var(--hover-light);
}

body.dark .nav-link-item .nav-link:hover {
  color: var(--accent-dark);
  background-color: var(--hover-dark);
}

/* Separator between nav items */
.main-nav .nav-link-item + .nav-link-item::before {
  content: "";
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  height: 20px;
  width: 1px;
  background-color: var(--border-light);
}

body.dark .main-nav .nav-link-item + .nav-link-item::before {
  background-color: var(--border-dark);
}

/* Projects Dropdown */
.projects-dropdown .dropdown-toggle {
  background: transparent !important;
  border: none;
  color: var(--text-light) !important;
  font-weight: 500;
}

body.dark .projects-dropdown .dropdown-toggle {
  color: var(--text-dark) !important;
}

.projects-dropdown .dropdown-toggle::after {
  margin-left: 8px;
}

.projects-dropdown .dropdown-menu {
  background-color: var(--dropdown-bg-light);
  border: none;
  border-radius: 8px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  padding: 0.5rem 0;
  min-width: 220px;
  margin-top: 10px;
}

body.dark .projects-dropdown .dropdown-menu {
  background-color: var(--dropdown-bg-dark);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
}

.dropdown-item-custom {
  padding: 0.75rem 1.5rem;
  color: var(--text-light) !important;
  font-weight: 500;
  transition: all 0.2s ease;
}

body.dark .dropdown-item-custom {
  color: var(--text-dark) !important;
}

.dropdown-item-custom:hover {
  background-color: var(--accent-light) !important;
  color: white !important;
}

body.dark .dropdown-item-custom:hover {
  background-color: var(--accent-dark) !important;
  color: white !important;
}

/* ================== RESPONSIVE DESIGN ================== */
/* --- FIXES FOR MOBILE VISIBILITY AND LOGO --- */

/* Mobile menu background like transparent water color */
@media (max-width: 991px) {
  .navbar-collapse {
    background: rgba(255, 255, 255, 0.8); /* light glassy background */
    backdrop-filter: blur(12px);
    border: 1px solid rgba(0, 0, 0, 0.05);
  }

  body.dark .navbar-collapse {
    background: rgba(0, 31, 63, 0.8); /* dark glassy background */
    border: 1px solid rgba(255, 255, 255, 0.1);
  }
}

/* Keep logo visible and balanced on small screens */
@media (max-width: 480px) {
  .logo-img {
    height: 100px !important; /* increase visibility */
    width: auto !important;
    display: block;
    margin: 0 auto; /* center it */
  }
}

/* Optional subtle floating effect on logo for a premium feel */
.logo-img:hover {
  transform: scale(1.05);
  filter: brightness(1.1);
}

</style>