<template>
  <div>
    <div class="border-right"></div>
    <div class="border-wrapper" ref="borderWrapper">

      <div class="bg-side"></div>

      <b-row class="main-row" no-gutters>
        <!-- Avatar Left -->
        <b-col md="4" class="relative group avatar-col">
          <b-img
            :src="avatar"
            id="avatar-img"
            alt="Murad Mursela Portrait"
            @mouseenter="changeAvatar"
            @mouseleave="changeAvatar"
            class="rounded-full shadow-2xl p-4 transition-transform duration-500 group-hover:scale-105"
          />
        </b-col>

        <!-- Intro Text -->
        <b-col md="8" class="intro-section">
          <div class="text-content">
            <div class="flex flex-col items-center justify-center animate__animated animate__fadeInUp animate__fast mt-12">
  <h3 class="text-2xl md:text-4xl font-semibold text-center">
    ARCHITECT | DESIGNER | INNOVATOR
  </h3>
  <h4 class="text-xl md:text-2xl font-medium text-center mt-2">
    MURAD MURSELA
  </h4>
</div>
            <div class="info">
              An <b>architect</b> and <b>graphic designer</b>, passionate about
              creating beautiful and functional designs.<br />
              I specialise in designing <b>logos</b>, <b>brochures</b>, and
              other visual identity materials for brands and projects.
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
        </b-col>
      </b-row>

      <!-- Social Icons -->
      <div class="social-icons animate__animated animate__fadeInUp animate__delay-1s">
        <social-link :to="socialLinks.github"><GithubIcon /></social-link>
        <social-link :to="socialLinks.linkedin"><LinkedinIcon /></social-link>
        <social-link :to="socialLinks.twitter"><TwitterIcon /></social-link>
        <social-link :to="socialLinks.facebook"><FacebookIcon /></social-link>
        <social-link :to="socialLinks.mail"><MailIcon /></social-link>
        <social-link :to="socialLinks.youtube" v-if="socialLinks.youtube"><YoutubeIcon /></social-link>
      </div>

      <!-- Background right overlay -->
      <div class="teletun-layer"></div>
    </div>

    <!-- Bottom-left logo + Telegram subscribe section -->
     <footer1 />
  </div>
</template>

<script>
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import LinkedinIcon from "vue-ionicons/dist/logo-linkedin.vue";
import TwitterIcon from "vue-ionicons/dist/logo-twitter.vue";
import FacebookIcon from "vue-ionicons/dist/logo-facebook.vue";
import YoutubeIcon from "vue-ionicons/dist/logo-youtube.vue";
import MailIcon from "vue-ionicons/dist/md-mail.vue";
import CallIcon from "vue-ionicons/dist/md-call.vue";

import logoWhite from "@/assets/mura-creatives-logo-white.png";
import logoBlack from "@/assets/mura-creatives-logo-black.png";

export default {
  components: {
    GithubIcon,
    LinkedinIcon,
    TwitterIcon,
    FacebookIcon,
    YoutubeIcon,
    MailIcon,
    CallIcon,
  },
  data() {
    return {
      avatar: require("@/assets/mi.png"),
      themeMode: "light",
      telegramInput: "",
      socialLinks: {
        github: "https://github.com/muradmursela",
        linkedin: "https://www.linkedin.com/in/muradmursela/",
        twitter: "https://twitter.com/muradmursela",
        facebook: "https://facebook.com/muradmursela",
        mail: "mailto:murad@example.com",
        youtube: "",
      },
    };
  },
  computed: {
    logoSrc() {
      return this.themeMode === "dark" ? logoWhite : logoBlack;
    },
  },
  methods: {
    changeAvatar() {
      this.avatar = require("@/assets/mi.png");
    },
    goToTelegram() {
      window.open("https://t.me/MuraCreatives", "_blank");
    },
  },
  mounted() {
    const saved = localStorage.themeMode;
    if (saved) {
      this.themeMode = saved;
    } else if (
      window.matchMedia &&
      window.matchMedia("(prefers-color-scheme: dark)").matches
    ) {
      this.themeMode = "dark";
    }
    document.body.classList.toggle("dark", this.themeMode === "dark");
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap");

.bottom-left-section {
  position: fixed;
  bottom: 2vh;
  left: 2vw;
  display: flex;
  align-items: flex-start;
  gap: 1.5vw;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.3); /* semi-transparent black */
  padding: 0.5rem 1rem; /* optional, for spacing around content */
  border-radius: 5px; /* optional, for rounded corners */
}


/* Logo */
.brand-logo {
  height: 8vh;
  width: 15vw;
  max-width: 200px;
  transition: transform 0.2s ease, opacity 0.3s ease;
}

.brand-logo:hover {
  transform: scale(1.1);
}

/* Telegram Subscribe Section */
.telegram-subscribe {
  display: flex;
  flex-direction: column;
  gap: 0.5vh;
  font-family: "Montserrat", sans-serif;
  font-size: 0.8rem;
  color: #ffffff;
}

body.dark .telegram-subscribe {
  color: #fff;
}

.telegram-subscribe p {
  margin: 0;
  font-weight: 500;
}

.telegram-subscribe input {
  padding: 0.5rem 0.75rem;
  border: 1px solid #bbb;
  border-radius: 0.4rem;
  outline: none;
  font-size: 0.75rem;
  width: 15vw;
  max-width: 250px;
  background-color: #f9f9f9;
  color: #222;
  transition: border-color 0.3s ease;
}

.telegram-subscribe input:focus {
  border-color: #929292;
}

body.dark .telegram-subscribe input {
  background-color: #222;
  border-color: #444;
  color: #fff;
}

.telegram-subscribe button {
  background-color: #929292;
  color: white;
  border: none;
  border-radius: 0.4rem;
  padding: 0.4rem 0;
  width: 5vw;
  min-width: 60px;
  cursor: pointer;
  font-size: 0.8rem;
  font-weight: 600;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

.telegram-subscribe button:hover {
  background-color: #686868;
  transform: scale(1.03);
}

/* Slogan styles */
.slogan {
  font-family: "Montserrat", sans-serif;
  font-size: 0.9rem;
  font-weight: 900;
  text-transform: uppercase;
  line-height: 1.3;
  letter-spacing: 0.05rem;
  color: #ffffff;
  max-width: 30vw;
  margin-top: 1vh;
}

.slogan h3 {
  margin: 0;
  padding: 0;
  font-size: inherit;
  font-weight: inherit;
  line-height: inherit;
}

body.dark .slogan {
  color: #ddd;
}

/* Contact styles */
.contact {
  font-family: "Montserrat", sans-serif;
  font-size: 0.8rem;
  color: #ffffff;
  max-width: 12vw;
}

body.dark .contact {
  color: #fff;
}

.contact h2 {
  font-size: 0.9rem;
  font-weight: 700;
  text-transform: uppercase;
  margin: 0 0 0.5rem 0;
  letter-spacing: 0.06rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 0.5vw;
  margin-bottom: 0.4vh;
  transition: transform 0.2s ease;
}

.contact-item:hover {
  transform: translateX(0.2vw);
}

.contact-icon {
  width: 1.2rem;
  height: 1.2rem;
  color: #555;
  transition: color 0.2s ease;
}

body.dark .contact-icon {
  color: #ccc;
}

.contact-item:hover .contact-icon {
  color: #929292;
}

.contact a {
  color: inherit;
  text-decoration: none;
  font-weight: 500;
}

.contact a:hover {
  text-decoration: underline;
}

/* General layout */
.border-wrapper {
  position: relative;
  overflow: visible;
  width: 100%;
  min-height: 100vh;
}

.border-bottom {
  padding-top: 1vh;
  position: absolute;
  left: 0;
  width: 100%;
  height: 8vh;
  background-image: url("@/assets/teletun.png");
  background-size: cover;
  bottom: -4vh;
  z-index: 1;
}

#avatar-img {
  width: 30vw;
  height: 67vh;
  max-width: 400px;
  max-height: 450px;
  object-fit: cover;
  animation: subtle-float-and-shift 4s infinite ease-in-out alternate;
  filter: drop-shadow(0.5vw 0.5vw 0.5vw rgba(140, 31, 243, 0.3));
  margin-right: 5vw;
  z-index: 99999;
}

.intro-section {
  display: flex;
  justify-content: flex-start;
}

.text-content {
  flex: 0 0 49vw;
  z-index: 3;
  margin-left: -10vw;
  padding: 2vw;
}

.intro {
  font-size: 2.5vw;
  line-height: 1.2;
}

.info {
  font-size: 1.2vw;
  margin-top: 2vh;
}

.action-btn {
  margin-top: 2vh;
  margin-right: 1vw;
  padding: 0.5rem 1.5rem;
  font-size: 1vw;
}

.bg-side {
  position: fixed;
  top: 0;
  right: 10vw;
  width: 25vw;
  height: 90vh;
  background-image: url("@/assets/bg.png");
  background-repeat: no-repeat;
  background-position: right top;
  background-size: cover;
  pointer-events: none;
  animation: slide-in-right 1.2s ease-out;
}

.teletun-layer {
  position: fixed;
  top: 0;
  right: 8vw;
  width: 5vw;
  height: 100vh;
  background-image: url("@/assets/teletun-min.png");
  background-repeat: no-repeat;
  background-position: right top;
  background-size: cover;
  z-index: 9998;
  pointer-events: none;
  animation: slide-in-right 1.2s ease-out;
}

/* Animations */
@keyframes subtle-float-and-shift {
  0%,
  100% {
    transform: scale(1.2) translate(0, 0) rotate(0deg);
  }
  50% {
    transform: scale(1.2) translate(0.2vw, -0.2vh) rotate(1deg);
  }
}

@keyframes slide-in-right {
  from {
    opacity: 0;
    transform: translateX(5vw);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Social Icons */
.social-icons {
  position: fixed;
  top: 20vh;
  left: 1.5vw;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 0.5vh;
  z-index: 1000;
}

.social-icons svg {
  width: 1.5rem;
  height: 1.5rem;
  cursor: pointer;
  transition: transform 0.3s;
}

.social-icons svg:hover {
  transform: scale(1.2);
}

/* Tablet Responsive (max-width: 1024px) */
@media (max-width: 1024px) {
  .border-wrapper {
    min-height: 100vh;
    height: auto;
  }

  .main-row {
    flex-direction: column;
    align-items: center;
    padding: 4vw;
  }

  .avatar-col {
    display: flex;
    justify-content: center;
    margin-bottom: 2vh;
  }

  #avatar-img {
    width: 40vw;
    height: 40vh;
    max-width: 300px;
    max-height: 300px;
    margin-right: 0;
  }

  .intro-section {
    justify-content: center;
    text-align: center;
    margin-left: 0;
  }

  .text-content {
    flex: 1;
    margin-left: 0;
    padding: 4vw;
  }

  .intro {
    font-size: 4vw;
  }

  .info {
    font-size: 2vw;
  }

  .action-btn {
    margin: 2vh 1vw;
    padding: 0.6rem 2rem;
    font-size: 1.8vw;
  }

  .bg-side,
  .teletun-layer,
  .border-bottom,
  .border-right {
    display: none;
  }

  .bottom-left-section {
    position: static;
    flex-direction: column;
    align-items: center;
    gap: 2vh;
    padding: 4vw;
    z-index: auto;
  }

  .brand-logo {
    height: 7vh;
    width: auto;
    max-width: 180px;
  }

  .telegram-subscribe {
    align-items: center;
    text-align: center;
  }

  .telegram-subscribe input {
    width: 50vw;
    max-width: 300px;
    font-size: 1.5vw;
  }

  .telegram-subscribe button {
    width: 20vw;
    max-width: 120px;
    font-size: 1.5vw;
    margin-top: 1vh;
  }

  .slogan {
    font-size: 1.5vw;
    text-align: center;
    max-width: 80vw;
    margin: 2vh auto;
  }

  .contact {
    font-size: 1.5vw;
    text-align: center;
    max-width: 80vw;
  }

  .contact h2 {
    font-size: 2vw;
  }

  .contact-item {
    justify-content: center;
  }

  .contact-icon {
    width: 2vw;
    height: 2vw;
  }

  .social-icons {
    position: static;
    flex-direction: row;
    justify-content: center;
    gap: 3vw;
    margin: 2vh 0;
    transform: none;
  }

  .social-icons svg {
    width: 3vw;
    height: 3vw;
  }
}

/* Mobile Responsive (max-width: 768px) */
@media (max-width: 768px) {
  .main-row {
    padding: 5vw;
    margin-top: 100px;
  }

  .avatar-col {
    display: none;
  }

  .intro {
    font-size: 5vw;
  }

  .info {
    font-size: 3vw;
  }

  .action-btn {
    width: 100%;
    margin: 2vh 0;
    font-size: 3vw;
  }

  .brand-logo {
    height: 6vh;
    max-width: 150px;
  }

  .telegram-subscribe input {
    width: 80vw;
    max-width: 90%;
    font-size: 3.5vw;
  }

  .telegram-subscribe button {
    width: 30vw;
    max-width: 100px;
    font-size: 3.5vw;
  }

  .slogan {
    font-size: 2.5vw;
    max-width: 90vw;
  }

  .contact {
    font-size: 2.5vw;
    max-width: 90vw;
  }

  .contact h2 {
    font-size: 3vw;
  }

  .contact-icon {
    width: 4vw;
    height: 4vw;
  }

  .social-icons svg {
    width: 5vw;
    height: 5vw;
  }
}

/* Extra small devices (max-width: 576px) */
@media (max-width: 576px) {
  .intro {
    font-size: 6vw;
  }

  .info {
    font-size: 3.5vw;
  }

  .action-btn {
    font-size: 3.5vw;
  }

  .slogan {
    font-size: 3vw;
  }

  .contact {
    font-size: 3vw;
  }

  .contact h2 {
    font-size: 3.5vw;
  }

  .telegram-subscribe input,
  .telegram-subscribe button {
    font-size: 4vw;
  }

  .social-icons svg {
    width: 6vw;
    height: 6vw;
  }
}

/* For same width (around 1280px) but smaller height: allow scrolling */
@media (min-width: 1280px) and (max-height: 1023px) {
  .border-wrapper {
    min-height: auto;
    height: auto;
  }
}
</style>