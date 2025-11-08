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
            <div class="photo-circle">
              <b-img :src="avatar" alt="Murad Mursela" class="photo-img" />
            </div>
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
            <img :src="telegramIcon" alt="Telegram" />
          </a>
          <a :href="socialLinks.instagram" target="_blank" class="pill">
            <img :src="instagramIcon" alt="Instagram" />
          </a>
          <a :href="`mailto:${socialLinks.mail}`" class="pill">
            <img :src="emailIcon" alt="Email" />
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
      telegramIcon: require("@/assets/telegram.png"),
      instagramIcon: require("@/assets/instagram.png"),
      emailIcon: require("@/assets/email.png"),
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
  --circle-bg: #e6f0ff;
  --overlay-rgba: rgba(255, 255, 255, 0.2);
  --bottom-bg: rgba(255, 255, 255, 0.5);
  --img-brightness: 1.2;
}
.dark {
  --bg-color: #001f3f;
  --text-color: #ffffff;
  --accent-color: #ff9f43;
  --circle-bg: #0f2850;
  --overlay-rgba: rgba(0, 0, 0, 0.3);
  --bottom-bg: rgba(0, 0, 0, 0.5);
  --img-brightness: 0.8;
}

/* Page wrapper */
.home-page {
  position: relative;
  font-family: "Montserrat", sans-serif;
  color: var(--text-color);
  min-height: 100vh;
  overflow-x: hidden;
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
  background: var(--circle-bg);
  border-radius: 50%;
  z-index: 0;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Main background image - hidden on smaller screens */
.bg-img {
  margin-top: 83px;
  width: 40%;
  height: 100%;
  object-fit: cover;
  position: relative;
  z-index: 1;
  filter: brightness(var(--img-brightness));
}

.overlay {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: var(--overlay-rgba);
  z-index: 2;
}

/* Main content wrapper */
.content-wrapper { 
  position: relative; 
  z-index: 10; 
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

/* MAIN WRAPPER */
.main-wrapper {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem 0;
}
.main-row { 
  width: 100%; 
  text-align: center; 
}

.text-col { 
  text-align: left; 
  padding-left: 4rem; 
}
.intro-text { 
  font-size: 2.8rem; 
  font-weight: 700; 
  margin-bottom: 0; 
}
.name-text { 
  font-size: 4.2rem; 
  font-weight: 900; 
  margin-top: 0; 
  line-height: 1; 
  color: var(--accent-color); 
}
.divider { 
  width: 100px; 
  border: 2px solid var(--accent-color); 
  margin: 1rem 0; 
}
.title-text { 
  font-size: 1.4rem; 
  font-weight: 600; 
  margin-bottom: 1rem; 
}
.bio-text { 
  font-size: 1rem; 
  line-height: 1.7; 
  max-width: 300px; 
}

/* Photo circle */
.photo-col { 
  display: flex; 
  justify-content: center; 
  align-items: center;
}
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
  overflow: hidden;
}
.photo-img { 
  width: 100%; 
  height: 100%; 
  object-fit: cover; 
}

/* Quote */
.quote-col { 
  text-align: right; 
  padding-right: 4rem; 
}
.quote-text { 
  font-size: 1.3rem; 
  font-style: italic; 
  opacity: 0.9; 
  color: var(--text-color); 
}

/* Bottom Section / Footer */
.bottom-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 2rem 1rem;
  background: var(--bottom-bg);
  border-radius: 20px;
  margin: 2rem auto;
  width: fit-content;
  backdrop-filter: blur(8px);
}
.join-telegram { 
  font-size: 1.3rem; 
  font-weight: 700; 
  margin-bottom: 1rem; 
  color: var(--accent-color); 
}

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

.footer-text { 
  font-size: 0.85rem; 
  color: #ff9900; 
  margin-top: 0.5rem; 
}

/* ================== RESPONSIVE DESIGN ================== */

/* Large laptops (992px - 1199px) */
@media (max-width: 1199px) {
  .bg-circle {
    width: 600px;
    height: 600px;
  }
  
  .photo-circle {
    width: 340px;
    height: 340px;
  }
  
  .intro-text { font-size: 2.5rem; }
  .name-text { font-size: 3.8rem; }
}

/* Tablets and small laptops (768px - 991px) */
@media (max-width: 991px) {
  .bg-img {
    display: none; /* Hide the background image on smaller screens */
  }
  
  .bg-circle {
    width: 500px;
    height: 500px;
  }
  
  .main-row { 
    flex-direction: column; 
    text-align: center;
  }
  
  .text-col, .quote-col { 
    text-align: center; 
    padding: 0 2rem; 
    margin-bottom: 2rem;
  }
  
  .photo-circle { 
    width: 300px; 
    height: 300px; 
    margin: 2rem 0; 
  }
  
  .bio-text { 
    max-width: 100%; 
    margin: 0 auto;
  }
  
  .intro-text { font-size: 2.2rem; }
  .name-text { font-size: 3.2rem; }
}

/* Mobile landscape and small tablets (576px - 767px) */
@media (max-width: 767px) {
  .bg-circle {
    width: 400px;
    height: 400px;
  }
  
  .text-col, .quote-col { 
    padding: 0 1.5rem; 
  }
  
  .photo-circle { 
    width: 280px; 
    height: 280px; 
  }
  
  .intro-text { font-size: 2rem; }
  .name-text { font-size: 2.8rem; }
  .title-text { font-size: 1.2rem; }
  
  .quote-text { 
    font-size: 1.1rem; 
    max-width: 300px;
    margin: 0 auto;
  }
  
  .bottom-section {
    padding: 1.5rem;
    margin: 1rem auto;
    width: 90%;
  }
}

/* Mobile phones (up to 575px) */
@media (max-width: 575px) {
  .bg-circle {
    width: 320px;
    height: 320px;
  }
  
  .text-col, .quote-col { 
    padding: 0 1rem; 
  }
  
  .photo-circle { 
    width: 250px; 
    height: 250px; 
  }
  
  .intro-text { font-size: 1.8rem; }
  .name-text { font-size: 2.4rem; }
  .title-text { font-size: 1.1rem; }
  
  .bio-text { 
    font-size: 0.9rem; 
  }
  
  .quote-text { 
    font-size: 1rem; 
  }
  
  .join-telegram { 
    font-size: 1.1rem; 
  }
  
  .pill {
    width: 45px;
    height: 45px;
  }
}
</style>