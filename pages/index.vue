<template>
  <div>
    <div class="border-right"></div>
    <div class="border-wrapper" ref="borderWrapper">
      <div class="border-bottom"></div>
      <div class="bg-side"></div>

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

        <!-- Intro Text -->
        <b-col md="2" class="intro-section">
          <div class="text-content">
            <h2 class="intro animate__animated animate__fadeInUp animate__fast">
              Hi,<br />
              I<span>'m Murad&nbsp;Mursela </span>.
            </h2>
            <div class="col-md-10 info">
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
        <social-link :to="socialLinks.youtube"><YoutubeIcon /></social-link>
      </div>

      <!-- Background right overlay -->
      <div class="teletun-layer"></div>
    </div>

    <!-- ✅ Bottom-left logo + Telegram subscribe section -->
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

    <!-- ✅ Bottom-right logo -->
    <div class="bottom-right-section">
      <div class="brand-logo-container">
        <img :src="logoSrc" alt="Mura Creatives Logo" class="brand-logo" />
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
  bottom: 25px;
  left: 35px;
  display: flex;
  align-items: flex-start;
  gap: 25px;
  z-index: 9999;
}

/* ✅ Bottom-right section */
.bottom-right-section {
  position: fixed;
  bottom: 25px;
  right: 0px;
  display: flex;
  align-items: flex-start;
  z-index: 9999;
}

/* ✅ Logo */
.brand-logo {
  height: 90px;
  width: 160px;
  transition: transform 0.2s ease, opacity 0.3s ease;
}
.brand-logo:hover {
  transform: scale(1.1);
}

/* ✅ Telegram Subscribe Section */
.telegram-subscribe {
  display: flex;
  flex-direction: column;
  gap: 6px;
  font-family: "Montserrat", sans-serif;
  font-size: 14px;
  color: #222; /* always visible in light */
}

body.dark .telegram-subscribe {
  color: #fff; /* always visible in dark mode */
}

.telegram-subscribe p {
  margin: 0;
  font-weight: 500;
}

.telegram-subscribe input {
  padding: 8px 12px;
  border: 1px solid #bbb;
  border-radius: 6px;
  outline: none;
  font-size: 13px;
  width: 230px;
  background-color: #f9f9f9;
  color: #222;
}

body.dark .telegram-subscribe input {
  background-color: #222;
  border-color: #444;
  color: #fff;
}

.telegram-subscribe button {
  background-color: #929292; /* Telegram blue */
  color: white;
  border: none;
  border-radius: 6px;
  padding: 6px 0;
  width: 50px; /* fixed width */
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

.telegram-subscribe button:hover {
  background-color: #686868;
  transform: scale(1.03);
}

/* ✅ Slogan styles - made smaller and improved */
.slogan {
  font-family: "Montserrat", sans-serif;
  font-size: 16px; /* Smaller font size */
  font-weight: 900; /* Slightly bolder for better readability */
  text-transform: uppercase;
  line-height: 1.3; /* Tighter line height for compactness */
  letter-spacing: 0.5px; /* subtle letter spacing for better aesthetics */
  color: #333; /* Darker color for light mode */
  max-width: 550px; /* Limit width to prevent sprawling */
  margin-top: 10px; /* Add some space from telegram section */
}

.slogan h3 {
  margin: 0;
  padding: 0;
  font-size: inherit; /* Inherit from parent */
  font-weight: inherit;
  line-height: inherit;
}

body.dark .slogan {
  color: #ddd; /* Lighter color for dark mode */
}

/* ✅ Contact styles - improved and beautiful */
.contact {
  font-family: "Montserrat", sans-serif;
  font-size: 14px;
  color: #222; /* Default for light mode */
  max-width: 200px; /* Limit width for better layout */
}

body.dark .contact {
  color: #fff; /* For dark mode */
}

.contact h2 {
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
  margin: 0 0 8px 0;
  letter-spacing: 1px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 6px;
  transition: transform 0.2s ease;
}

.contact-item:hover {
  transform: translateX(4px);
}

.contact-icon {
  width: 20px;
  height: 20px;
  color: #555; /* Slightly muted for light mode */
  transition: color 0.2s ease;
}

body.dark .contact-icon {
  color: #ccc; /* Muted for dark mode */
}

.contact-item:hover .contact-icon {
  color: #929292; /* Match telegram button color on hover */
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
  overflow: hidden;
}

.border-bottom {
  padding-top: 10px;
  position: absolute;
  left: 0;
  width: 100%;
  height: 80px;
  background-image: url("@/assets/teletun.png");
  bottom: -30px;
  z-index: 1;
}

#avatar-img {
  width: 350px;
  height: 380px;
  object-fit: cover;
  animation: subtle-float-and-shift 4s infinite ease-in-out alternate;
  filter: drop-shadow(10px 10px 10px rgba(140, 31, 243, 0.3));
  margin-right: 100px;
}

.intro-section {
  display: flex;
  justify-content: flex-start;
}

.text-content {
  flex: 0 0 800px;
  z-index: 3;
  margin-left: -200px;
}

.bg-side {
  position: fixed;
  top: 0;
  right: 200px;
  width: 400px;
  height: 500px;
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
  right: 160px;
  width: 5%;
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
    transform: scale(1.2) translate(2px, -2px) rotate(1deg);
  }
}

@keyframes slide-in-right {
  from {
    opacity: 0;
    transform: translateX(100px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Social Icons */
.social-icons {
  position: fixed;
  top: 20%;
  left: 20px;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 5px;
  z-index: 1000;
}

.social-icons svg {
  width: 28px;
  height: 28px;
  cursor: pointer;
  transition: transform 0.3s;
}
.social-icons svg:hover {
  transform: scale(1.2);
}

/* Mobile Responsive */
@media (max-width: 768px) {
  #avatar-img,
  .bg-side,
  .teletun-layer,
  .border-bottom,
  .border-right {
    display: none;
  }

  .bottom-left-section {
    flex-direction: column;
    align-items: center;
    bottom: 15px;
    left: 15px;
    gap: 15px;
  }

  .bottom-right-section {
    flex-direction: column;
    align-items: center;
    bottom: 15px;
    right: 15px;
  }

  .brand-logo {
    height: 70px;
  }

  .telegram-subscribe input,
  .telegram-subscribe button {
    width: 180px;
  }

  .social-icons {
    position: static;
    flex-direction: row;
    justify-content: center;
    margin-top: 20px;
  }

  .slogan {
    font-size: 10px; /* Even smaller on mobile */
    text-align: center;
    max-width: 200px;
  }

  .contact {
    font-size: 12px;
    text-align: center;
  }

  .contact h2 {
    font-size: 14px;
  }

  .contact-icon {
    width: 18px;
    height: 18px;
  }

  .contact-item {
    justify-content: center;
  }
}
</style>