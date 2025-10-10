<template>
  <div>
    <div class="border-right"></div>
    <div class="border-wrapper" ref="borderWrapper">
      <div class="border-bottom"></div>

      <b-row class="main-row" no-gutters>
      
        <!-- Avatar Left -->
        <b-col md="4" class="relative group">
          <b-img
            :src="avatar"
            id="avatar-img"
            alt="Murad Mursela Portrait"
            @mouseenter="changeAvatar"
            @mouseleave="changeAvatar"
            class="rounded-full shadow-2xl p-4 transition-transform duration-500 group-hover:scale-105"
          />
        </b-col>

        <!-- Intro Text + BG Right -->
        <b-col md="8" class="intro-section">
          <div class="text-content">
            <h2 class="intro animate__animated animate__fadeInUp animate__fast">
              Hi,<br />
              I<span>'m Murad&nbsp;Mursela</span>.
            </h2>
            <div class="col-md-10 info">
              An <b>architect</b> and <b>graphic designer</b>, passionate about
              creating beautiful and functional designs.<br />
              I specialise in designing <b>logos</b>, <b>brochures</b>, and other
              visual identity materials for brands and projects.
              <br />
              <b-button
                class="action-btn animate__animated animate__wobble animate__delay-4s animate__fast"
                to="/projects"
              >
                Explore >
              </b-button>
              <b-button class="action-btn" to="/contact" variant="primary">
                Get In Touch
              </b-button>
            </div>
          </div>

          <!-- Background Image (Right beside text) -->
          <div class="bg-side"></div>
        </b-col>
      </b-row>

      <!-- Social Icons -->
      <div class="social-icons animate__animated animate__fadeInUp animate__delay-1s">
        <social-link :to="socialLinks.github"><GithubIcon /></social-link>
        <social-link :to="socialLinks.linkedin"><LinkedinIcon /></social-link>
        <social-link :to="socialLinks.twitter"><TwitterIcon /></social-link>
        <social-link :to="socialLinks.facebook"><FacebookIcon /></social-link>
        <social-link :to="socialLinks.mail"><MailIcon /></social-link>
        <social-link :to="socialLinks.youtube"><YoutubeIcon /></social-link>
      </div>

      <!-- 🔹 4th Layer: teletun-min.png (Full Screen Right Corner Overlay) -->
      <div class="teletun-layer"></div>
    </div>
  </div>
</template>

<script>
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import LinkedinIcon from "vue-ionicons/dist/logo-linkedin.vue";
import TwitterIcon from "vue-ionicons/dist/logo-twitter.vue";
import FacebookIcon from "vue-ionicons/dist/logo-facebook.vue";
import YoutubeIcon from "vue-ionicons/dist/logo-youtube.vue";
import MailIcon from "vue-ionicons/dist/md-mail.vue";

export default {
  components: {
    GithubIcon,
    LinkedinIcon,
    TwitterIcon,
    FacebookIcon,
    YoutubeIcon,
    MailIcon
  },
  data() {
    return {
      avatar: require("@/assets/mi.png"),
      socialLinks: {
        github: "https://github.com/muradmursela",
        linkedin: "https://www.linkedin.com/in/muradmursela/",
        twitter: "https://twitter.com/muradmursela",
        facebook: "https://facebook.com/muradmursela",
        mail: "mailto:murad@example.com",
        youtube: ""
      }
    };
  },
  head: {
    title: "Portfolio ⚡ - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Murad Mursela is an amazing architect and graphic designer, passionate about creating logos, brochures, and visual identities for brands and projects."
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Portfolio ⚡ - Murad Mursela"
      },
      {
        property: "og:description",
        content:
          "Murad Mursela is an amazing architect and graphic designer, passionate about creating logos, brochures, and visual identities for brands and projects."
      }
    ]
  },
  methods: {
    changeAvatar() {
      this.avatar = require("@/assets/mi.png");
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

.border-wrapper {
  position: relative;
  overflow: hidden;
}

/* Bottom Border */
.border-bottom {
  position: absolute;
  left: 0;
  width: 100%;
  height: 80px;
  background-image: url("@/assets/teletun.png");
  background-repeat: repeat-x;
  background-size: auto 100%;
  background-position: center;
  bottom: -30px;
  z-index: 1;
}

/* Main Row Spacing — Narrower gap between avatar, text, and bg */


/* Avatar */
#avatar-img {
  width: 280px;
  height: 560px;
  object-fit: cover;
  border-radius: 50%;
  animation: subtle-float-and-shift 4s infinite ease-in-out alternate;
  filter: drop-shadow(0 0 10px rgba(138, 43, 226, 0.3));
}

/* Intro + BG layout */
.intro-section {
  position: relative;
  display: flex;
  
  justify-content: space-between;
/* 🔹 Reduced gap between text and bg */

}

.text-content {
  flex: 1;
  padding-right: 0;
  z-index: 3;
}

/* Background image right (bg.png) */
.bg-side {
  flex: 0 0 220px;
  height: 420px;
  background-image: url("@/assets/bg.png");
  background-size: cover;
  background-position: left;
  background-repeat: no-repeat;
  border-radius: 20px;
  
  animation: fade-in 1.5s ease-in-out;
  z-index: 2;
}

/* 🔹 4th layer: teletun-min.png fully aligned right corner */
.teletun-layer {
  position: fixed;
  top: 0;
  right: 0;
  width: 3%;
  height: 100vh;
  background-image: url("@/assets/teletun-min.png");
  background-repeat: no-repeat;
  background-position: right top;
  background-size: cover;
  z-index: 9999; /* Always on top */
  pointer-events: none; /* Don’t block clicks */
  animation: slide-in-right 1.2s ease-out;
}

/* Animations */
@keyframes subtle-float-and-shift {
  0%, 100% { transform: scale(1.2) translate(0, 0) rotate(0deg); }
  50% { transform: scale(1.2) translate(2px, -2px) rotate(1deg); }
}

@keyframes fade-in {
  from { opacity: 0; transform: translateX(50px); }
  to { opacity: 1; transform: translateX(0); }
}

@keyframes slide-in-right {
  from { opacity: 0; transform: translateX(100px); }
  to { opacity: 1; transform: translateX(0); }
}

/* Social Icons */
.social-icons {
  position: fixed;
  top: 20%;
  left: 20px;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 8px; /* 🔹 slightly tighter gap */
  z-index: 1000;
}

.social-icons svg {
  width: 28px;
  height: 28px;
  cursor: pointer;
  transition: transform 0.3s;
}
.social-icons svg:hover { transform: scale(1.2); }

/* Fonts */
.intro {
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
}
.info {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
}

/* Mobile */
@media (max-width: 768px) {
  #avatar-img { display: none; }
  .bg-side { display: none; }
  .teletun-layer { display: none; }
  .border-bottom, .border-right, .border-left, .border-top { display: none; }
  b-col { width: 100%; }
  .social-icons {
    position: static;
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-top: 20px;
  }
  .social-icons svg { width: 24px; height: 24px; }
}
</style>