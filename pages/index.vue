<template>
  <div class="border-wrapper" ref="borderWrapper">
    <div class="border-top"></div>
    <div class="border-bottom"></div>
    <div class="border-left" :style="{ width: verticalWidth + 'px' }"></div>
    <div class="border-right" :style="{ width: verticalWidth + 'px' }"></div>
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
          Hi 👋,
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

          <!-- .SOCIAL LINKS SECTION -->
          <div
            class="social-icons animate__animated animate__fadeInUp animate__delay-1s"
          >
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
      </b-col>
    </b-row>
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
      },
      verticalWidth: 0
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
  },

  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
      setTimeout(() => this.$nuxt.$loading.finish(), 500);

      const root = this.$refs.borderWrapper;
      const style = getComputedStyle(root);
      const borderSize = parseFloat(style.getPropertyValue('--border-size'));
      this.verticalWidth = root.clientHeight + 2 * borderSize;
    });
  }
};
</script>

<style scoped>
.border-wrapper {
  position: relative;
  --border-size: 80px;
}

/* Top and bottom borders */
.border-top,
.border-bottom {
  position: absolute;
  left: 0;
  width: 100%;
  height: var(--border-size);
  background-image: url("@/assets/tiletu.png");
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

/* Vertical borders */
.border-left,
.border-right {
  position: absolute;
  top: calc(-1 * var(--border-size));
  height: var(--border-size);
  background-image: url("@/assets/tiletu.png");
  background-repeat: repeat-x;
  background-size: auto 100%;
  background-position: center;
}

.border-left {
  left: 0;
  transform: rotate(90deg);
  transform-origin: top left;
}

.border-right {
  right: 0;
  transform: rotate(90deg);
  transform-origin: top right;
}

/* Glowing background behind transparent PNG avatar */
#avatar-img::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 9999px; /* same as rounded-full */
  background: linear-gradient(135deg, #ff7f50, #ff1493, #8a2be2);
  filter: blur(20px);
  opacity: 0.6;
  z-index: -1; /* behind the image */
  transition: all 0.5s ease;
}

.group:hover #avatar-img::before {
  filter: blur(30px);
  opacity: 0.8;
}

@media (max-width: 768px) {
  .border-wrapper {
    --border-size: 40px;
  }
}
</style>