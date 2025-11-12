<template>
  <div>
    <!-- Fixed Navbar -->
    <NavBar />

    <!-- Main App Content -->
    <div id="app">
      <Nuxt />
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/NavBar.vue";

export default {
  name: "DefaultLayout",
  components: { NavBar },
};
</script>

<style>
/* ===============================
   Global layout styling
   Keeps spacing below navbar
==============================

/* Mobile view extra spacing */
@media (max-width: 991px) {
  #app {
    padding-top: 120px; /* slightly more space for smaller screens */
  }
}

/* Optional: add a soft fade shadow under navbar */
body::before {
  content: "";
  position: fixed;
  top: 100px;
  left: 0;
  width: 100%;
  height: 10px;
  background: linear-gradient(to bottom, rgba(0,0,0,0.1), transparent);
  pointer-events: none;
  z-index: 1999;
}

@media (max-width: 991px) {
  body::before {
    top: 120px;
  }
}
</style>
