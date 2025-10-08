<template>
<div>
  <div class="border-right"></div>
  <div class="border-wrapper" ref="borderWrapper">
    <div class="border-bottom"></div>
    <b-row style="margin-left: 0;margin-right: 0;">
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
      <b-col md="8">
        <h2 class="intro animate__animated animate__fadeInUp animate__fast">
          Hi,
          <br />I<span>'m Murad&nbsp;Mursela</span>.
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
      </b-col>
    </b-row>

    <div class="social-icons animate__animated animate__fadeInUp animate__delay-1s">
      <social-link :to="socialLinks.github">
        <GithubIcon />
      </social-link>

      <social-link :to="socialLinks.linkedin">
        <LinkedinIcon />
      </social-link>

      <social-link :to="socialLinks.twitter">
        <TwitterIcon />
      </social-link>

      <social-link :to="socialLinks.facebook">
        <FacebookIcon />
      </social-link>

      <social-link :to="socialLinks.mail">
        <MailIcon />
      </social-link>

      <social-link :to="socialLinks.youtube">
        <YoutubeIcon />
      </social-link>
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
      },

    ]
  },

  methods: {
    changeAvatar() {
      this.avatar =
        this.avatar === require("@/assets/mi.png")
          ? require("@/assets/mi.png")
          : require("@/assets/mi.png");
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

.border-wrapper {
  position: relative;
}

.border-bottom {
  position: absolute;
  left: 0;
  width: 100%;
  height: 80px;
  background-image: url("@/assets/teletun.png");
  background-repeat: repeat-x;
  background-size: auto 100%;
  background-position: center;
}

.border-top {
  top: calc(-1 * var(--border-size));
}

.border-bottom {
  bottom: -30px;
  z-index: 1;
}



/* ----------------------------- */
/* Avatar size + animation tweaks */
/* ----------------------------- */
#avatar-img {
  width: 280px;       /* smaller size */
  height: 560px;
  object-fit: cover;
  border-radius: 50%;
  animation: subtle-float-and-shift 4s infinite ease-in-out alternate;
  filter: drop-shadow(0 0 10px rgba(138, 43, 226, 0.3));
}

#avatar-img::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 9999px;
  background: linear-gradient(135deg, #ff7f50, #ff1493, #8a2be2);
  filter: blur(70px);
  opacity: 0.6;
  z-index: -1;
  transition: all 0.5s ease;
  animation: glow-pulse 2s infinite ease-in-out;
}

.group:hover #avatar-img {
  filter: drop-shadow(0 0 15px rgba(138, 43, 226, 0.5));
}

.group:hover #avatar-img::before {
  filter: blur(30px);
  opacity: 0.8;
}

/* ------------------------------------------- */
/* Animation: subtle floating with smaller zoom */
/* ------------------------------------------- */
@keyframes subtle-float-and-shift {
  0% {
    transform: scale(1.2) translate(0px, 0px) rotate(0deg);
  }
  15% {
    transform: scale(1.2) translate(1px, -1.5px) rotate(0.8deg);
  }
  30% {
    transform: scale(1.2) translate(2px, 0.5px) rotate(-1deg);
  }
  45% {
    transform: scale(1.2) translate(0.5px, -0.5px) rotate(0.2deg);
  }
  60% {
    transform: scale(1.2) translate(-1.5px, -1px) rotate(1.5deg);
  }
  75% {
    transform: scale(1.2) translate(-0.5px, 1px) rotate(-0.5deg);
  }
  90% {
    transform: scale(1.2) translate(0.25px, -0.25px) rotate(0.1deg);
  }
  100% {
    transform: scale(1.2) translate(0px, 0px) rotate(0deg);
  }
}

/* Glow pulse effect */
@keyframes glow-pulse {
  0%, 100% {
    opacity: 0.6;
    filter: blur(20px);
  }
  50% {
    opacity: 0.7;
    filter: blur(25px);
  }
}

/* Social Icons Fixed Left */
.social-icons {
  position: fixed;
  top: 20%;
  left: 20px;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 15px;
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

/* Font styles */
.intro {
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
}

.info {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
}

/* Mobile adjustments */
@media (max-width: 768px) {
  .border-wrapper {
    --border-size: 40px;
  }

  .border-bottom,
  .border-right,
  .border-left,
  .border-top {
    display: none;
  }

  #avatar-img {
    width: 140px;
    height: 140px;
  }

  b-col {
    width: 100%;
  }

  .social-icons {
    position: static;
    top: auto;
    left: auto;
    transform: none;
    display: flex;
    flex-direction: row;
    gap: 15px;
    justify-content: center;
    margin-top: 20px;
    z-index: auto;
  }

  .social-icons svg {
    width: 24px;
    height: 24px;
  }
}
</style>
