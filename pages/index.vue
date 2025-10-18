<template>
  <div>
    <div class="border-right"></div>
    <div class="border-wrapper" ref="borderWrapper">
      <div class="border-bottom"></div>
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
            <h2 class="intro animate__animated animate__fadeInUp animate__fast">
             
             <h3> ARCHITECT | DESIGNER | INNOVATOR </h3>
             <h4>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MURAD MURSELA</h4>
            </h2>
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
    <div class="bottom-left-section">
      <div class="brand-logo-container">
        <img :src="logoSrc" alt="Mura Creatives Logo" class="brand-logo" />
      </div>

      <div class="telegram-subscribe">
        <p>Subscribe to our Telegram channel</p>
        <input
          type="text"
          v-model="telegramInput"
          placeholder="Enter your Telegram username"
        />
        <button @click="goToTelegram">Join</button>
      </div>
      <div class="slogan">
        <h3>THE DIFFERENCE BETWEEN</h3>
        <h3> GOOD AND BAD</h3>
        <h3> ARCHITECTURE IS THE TIME YOU SPEND YOUR TIME ON IT</h3>
      </div>
      <div class="contact">
        <h2>Contact</h2>
        <div class="contact-item">
          <CallIcon class="contact-icon" />
          <a href="tel:+251947485789">+251 947 485 789</a>
        </div>
        <div class="contact-item">
          <CallIcon class="contact-icon" />
          <a href="tel:+251968414867">+251 968 414 867</a>
        </div>
      </div>
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
  bottom: 12vh;
}

/* Bottom-right section */
.bottom-right-section {
  position: fixed;
  bottom: 2vh;
  right: 0;
  display: flex;
  align-items: flex-start;
  z-index: 9999;
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
  color: #222;
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
  width: 3vw;
  min-width: 50px;
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
  color: #333;
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
  color: #222;
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
  overflow: visible; /* Allow scrolling if content overflows */
  width: 100%;
  min-height: 100vh; /* Changed to min-height to allow expansion */
}

.border-bottom {
  padding-top: 1vh;
  position: absolute;
  left: 0;
  width: 100%;
  height: 8vh;
  background-image: url("@/assets/teletun.png");
  background-size: cover;
  bottom: -8vh;
  z-index: 1;
}

#avatar-img {
  width: 30vw;
  height: 47vh;
  max-width: 400px;
  max-height: 450px;
  object-fit: cover;
  animation: subtle-float-and-shift 4s infinite ease-in-out alternate;
  filter: drop-shadow(0.5vw 0.5vw 0.5vw rgba(140, 31, 243, 0.3));
  margin-right: 5vw;
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
  width: 20vw;
  height: 70vh;
  background-image: url("@/assets/bg.png");
  background-repeat: no-repeat;
  background-position: right top;
  background-size: cover;
  z-index: 9998;
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

/* Media query for widths not exactly 1280px - hide specific images */
@media (min-width: 1281px), (max-width: 1279px) {
  .border-bottom,
  .bg-side,
  .teletun-layer {
    display: none;
  }

  /* Adjustments for other elements to look good */
  .text-content {
    margin-left: 0;
    padding: 1vw;
    flex: 1;
  }

  .intro {
    font-size: 2rem;
  }

  .info {
    font-size: 1rem;
  }

  .action-btn {
    font-size: 0.9rem;
  }

  #avatar-img {
    width: 25vw;
    height: auto;
    max-width: 350px;
    margin-right: 2vw;
  }

  .bottom-left-section {
    gap: 1vw;
    bottom: 5vh;
  }

  .brand-logo {
    height: 6vh;
    width: auto;
    max-width: 150px;
  }

  .telegram-subscribe {
    font-size: 0.7rem;
  }

  .telegram-subscribe input {
    width: 12vw;
    max-width: 200px;
    font-size: 0.7rem;
  }

  .telegram-subscribe button {
    width: 4vw;
    min-width: 40px;
    font-size: 0.7rem;
  }

  .slogan {
    font-size: 0.8rem;
    max-width: 25vw;
  }

  .contact {
    font-size: 0.7rem;
    max-width: 10vw;
  }

  .contact h2 {
    font-size: 0.8rem;
  }

  .contact-icon {
    width: 1rem;
    height: 1rem;
  }

  .social-icons {
    gap: 0.4vh;
  }

  .social-icons svg {
    width: 1.2rem;
    height: 1.2rem;
  }
}

/* Mobile Responsive - already present, but enhanced for better flow */
@media (max-width: 768px) {
  .main-row {
    flex-direction: column;
    align-items: center;
    padding: 2vw;
  }

  .avatar-col {
    display: none;
  }

  .intro-section {
    justify-content: center;
    text-align: center;
    margin-left: 0;
  }

  .text-content {
    flex: 1;
    margin-left: 0;
    padding: 2vw;
  }

  .intro {
    font-size: 4vw;
  }

  .info {
    font-size: 2.5vw;
  }

  .action-btn {
    width: 100%;
    margin: 2vh 0;
    font-size: 2.5vw;
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
    padding: 2vw;
    bottom: auto;
    left: auto;
    z-index: auto;
  }

  .bottom-right-section {
    display: none;
  }

  .brand-logo {
    height: 7vh;
    width: auto;
    max-width: 150px;
  }

  .telegram-subscribe {
    align-items: center;
    text-align: center;
  }

  .telegram-subscribe input,
  .telegram-subscribe button {
    width: 100%;
    max-width: 80vw;
    font-size: 2.5vw;
  }

  .telegram-subscribe button {
    width: 100%;
    max-width: 80vw;
    margin-top: 1vh;
  }

  .slogan {
    font-size: 2vw;
    text-align: center;
    max-width: 90vw;
    margin: 2vh auto;
  }

  .contact {
    font-size: 2vw;
    text-align: center;
    max-width: 90vw;
  }

  .contact h2 {
    font-size: 2.5vw;
  }

  .contact-item {
    justify-content: center;
  }

  .contact-icon {
    width: 3vw;
    height: 3vw;
  }

  .social-icons {
    position: static;
    flex-direction: row;
    justify-content: center;
    gap: 2vw;
    margin: 2vh 0;
    transform: none;
  }

  .social-icons svg {
    width: 5vw;
    height: 5vw;
  }
}

/* Extra small devices (phones, less than 576px) */
@media (max-width: 575px) {
  .intro {
    font-size: 5vw;
  }

  .info {
    font-size: 3vw;
  }

  .slogan {
    font-size: 2.5vw;
  }

  .contact {
    font-size: 2.5vw;
  }

  .telegram-subscribe input,
  .telegram-subscribe button {
    font-size: 3vw;
  }
}

/* For same width (around 1280px) but smaller height: allow scrolling by using min-height */
@media (min-width: 1280px) and (max-height: 1023px) {
  .border-wrapper {
    min-height: auto; /* Let it expand naturally */
    height: auto; /* Allow height to grow beyond viewport */
  }
}
</style>