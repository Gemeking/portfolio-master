<template>
  <div class="border-wrapper" ref="borderWrapper">
    <!-- Top & Bottom (horizontal pattern) -->
    <div class="border-bottom"></div>

    <!-- Left & Right (vertical pattern) -->
    <div class="border-right"></div>

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

    <!-- .SOCIAL LINKS SECTION (fixed left, vertical) -->
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
      {
        hid: "og:image",
        name: "og:image",
        content: require("@/assets/coding.png")
      }
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
.border-wrapper {
  position: relative;
  --border-size: 80px;
}


.border-bottom {
  position: absolute;
  left: 0;
  width: 100%;
  height: var(--border-size);
  background-image: url("@/assets/teletun.png");
  background-repeat: repeat-x;
  background-size: auto 100%;
  background-position: center;
}

.border-top {
  top: calc(-1 * var(--border-size));
}

.border-bottom {
  bottom: calc(-1 * var(--border-size));
}

.border-left,
.border-right {
  position: absolute;
  top: 0;
  z-index: 9999;
  height: 100%;
  width: var(--border-size);
  background-image: url("@/assets/teletun-min.png");
  background-repeat: repeat-y;
  background-size: 100% auto;
  background-position: center;
}

.border-left {
  left: calc(-1 * var(--border-size));
}

.border-right {
  /* moved inward a bit */
  right: 20px; 
  z-index: 1;
}
.border-bottom{
  bottom: 20px;
  z-index: 1;
}


/* Avatar glow */
#avatar-img::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 9999px;
  background: linear-gradient(135deg, #ff7f50, #ff1493, #8a2be2);
  filter: blur(20px);
  opacity: 0.6;
  z-index: -1;
  transition: all 0.5s ease;
}

.group:hover #avatar-img::before {
  filter: blur(30px);
  opacity: 0.8;
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

@media (max-width: 768px) {
  .border-wrapper {
    --border-size: 40px;
  }

  /* Hide borders */
  .border-bottom,
  .border-right,
  .border-left,
  .border-top {
    display: none;
  }

  /* Hide avatar image */
  #avatar-img {
    display: none;
  }

  /* Adjust columns for mobile */
  b-col {
    width: 100%;
  }

  /* Social icons below content, horizontal */
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