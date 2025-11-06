<template>
  <div :class="themeMode" class="home-page">
    <!-- Full-page background image -->
    <div class="background-image">
      <!-- Circular background -->
      <div class="bg-circle"></div>
      <b-img :src="avatar" alt="Murad Mursela" class="bg-img" />
      <div class="overlay"></div>
    </div>

    <!-- Main content -->
    <div class="content-wrapper">
      <div class="main-wrapper">
        <b-row class="main-row" no-gutters align-v="center" align-h="center">
          <!-- Left text -->
          <b-col md="3" class="text-col">
            <h1 class="intro-text">I'm</h1>
            <h1 class="name-text">MURAD MURSELA</h1>
            <hr class="divider" />
            <h2 class="title-text">ARCHITECT / GRAPHIC DESIGNER</h2>
            <p class="bio-text">
              An architect and graphic designer, passionate about creating beautiful
              and functional designs. I specialize in designing logos, brochures, and
              visual identities for brands and projects.
            </p>
          </b-col>

          <!-- Center: Photo circle -->
          <b-col md="6" class="photo-col">
           
          </b-col>

          <!-- Right: Quote -->
          <b-col md="3" class="quote-col">
            <p class="quote-text">"Architecture is the time you spend your time on it."</p>
          </b-col>
        </b-row>
      </div>

      <!-- Bottom section / Footer -->
      <div class="bottom-section">
        <div class="join-telegram">Connect With Me</div>
        <div class="social-pills">
          <a :href="socialLinks.telegram" target="_blank" class="pill">
            <img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" alt="Telegram" />
          </a>
          <a :href="socialLinks.instagram" target="_blank" class="pill">
            <img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" alt="Instagram" />
          </a>
          <a :href="`mailto:${socialLinks.mail}`" class="pill">
            <img src="https://cdn-icons-png.flaticon.com/512/732/732200.png" alt="Email" />
          </a>
        </div>
        <p class="footer-text">© {{ new Date().getFullYear() }} Murad Mursela. All Rights Reserved.</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomePage",
  data() {
    return {
      avatar: require("@/assets/murilo.png"),
      socialLinks: {
        instagram: "https://www.instagram.com/mura_abdo",
        telegram: "https://t.me/Murilo81",
        mail: "muradmursela@gmail.com",
      },
      themeMode: "light",
    };
  },
  mounted() {
    if (process.client) {
      const savedMode = localStorage.getItem("themeMode");
      if (savedMode) this.themeMode = savedMode;
      else if (window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches)
        this.themeMode = "dark";

      document.body.classList.toggle("dark", this.themeMode === "dark");
    }
  },
  methods: {
    toggleDarkMode() {
      if (process.client) {
        this.themeMode = this.themeMode === "dark" ? "light" : "dark";
        document.body.classList.toggle("dark", this.themeMode === "dark");
        localStorage.setItem("themeMode", this.themeMode);
      }
    },
  },
};
</script>

<style scoped>
/* Fonts */
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap");

/* THEME VARIABLES */
.light {
  --bg-color: #ffffff;
  --text-color: #111111;
  --accent-color: #001f3f;
}
.dark {
  --bg-color: #001f3f;
  --text-color: #ffffff;
  --accent-color: #ff9f43;
}

/* Page wrapper */
.home-page {
  position: relative;
  font-family: "Montserrat", sans-serif;
  color: var(--text-color);
}

/* Full-screen background image */
.background-image {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Circular background behind image */
.bg-circle {
  position: absolute;
  width: 700px;
  height: 700px;
  background: #0f2850; /* light accent circle */
  border-radius: 50%;
  z-index: 0;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

}

/* Main background image */
.bg-img {
  margin-top: 83px;
  width: 40%;
  height: 100%;
  object-fit: cover;
  position: relative;
  z-index: 1;
}

.overlay {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.3);
  z-index: 2;
}

/* Main content wrapper */
.content-wrapper { position: relative; z-index: 10; }

/* MAIN WRAPPER */
.main-wrapper {
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 4rem 0;
}
.main-row { width: 100%; text-align: center; }

.text-col { text-align: left; padding-left: 4rem; }
.intro-text { font-size: 2.8rem; font-weight: 700; margin-bottom: 0; }
.name-text { font-size: 4.2rem; font-weight: 900; margin-top: 0; line-height: 1; color: var(--accent-color); }
.divider { width: 100px; border: 2px solid var(--accent-color); margin: 1rem 0; }
.title-text { font-size: 1.4rem; font-weight: 600; margin-bottom: 1rem; }
.bio-text { font-size: 1rem; line-height: 1.7; max-width: 300px; }

/* Photo circle */
.photo-col { display: flex; justify-content: center; }
.photo-circle {
  background-color: var(--bg-color);
  border-radius: 50%;
  width: 380px;
  height: 380px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 25px rgba(0,0,0,0.5);
  transition: all 0.4s ease;
}
.photo-img { width: 90%; height: 90%; object-fit: cover; border-radius: 50%; }

/* Quote */
.quote-col { text-align: right; padding-right: 4rem; }
.quote-text { font-size: 1.3rem; font-style: italic; opacity: 0.9; color: #fff; }

/* Bottom Section / Footer */
.bottom-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 2rem 1rem;
  background: rgba(0,0,0,0.5);
  border-radius: 20px;
  margin: 2rem auto;
  width: fit-content;
  backdrop-filter: blur(8px);
}
.join-telegram { font-size: 1.3rem; font-weight: 700; margin-bottom: 1rem; color: var(--accent-color); }

/* Social icons as images */
.social-pills {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 1rem;
}
.pill {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
  transition: all 0.3s ease;
  background: var(--accent-color);
}
.pill img {
  width: 70%;
  height: 70%;
  object-fit: contain;
}
.pill:hover {
  transform: scale(1.2);
  filter: brightness(1.2);
}

.footer-text { font-size: 0.85rem; color: #ccc; margin-top: 0.5rem; }

/* Responsive */
@media (max-width: 991px) {
  .main-row { flex-direction: column; }
  .text-col, .quote-col { text-align: center; padding: 0 2rem; }
  .photo-circle { width: 300px; height: 300px; margin: 2rem 0; }
}
@media (max-width: 480px) {
  .intro-text { font-size: 2rem; }
  .name-text { font-size: 2.8rem; }
  .photo-circle { width: 250px; height: 250px; }
}
</style>
