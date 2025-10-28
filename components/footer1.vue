<template>
  <footer class="footer-wrapper animate__animated animate__fadeInUp">
    <div class="footer-container container">
      <!-- LEFT SIDE: BRAND + TELEGRAM -->
      <div class="footer-left">
        <div class="brand-logo-container">
          <img :src="logoSrc" alt="Mura Creatives Logo" class="brand-logo" />
        </div>

        <div class="telegram-subscribe">
          <p>Join our <strong>Telegram Channel</strong></p>
          <button @click="goToTelegram" class="telegram-btn">
            Join Now
          </button>
        </div>
      </div>

      <!-- CENTER: SLOGAN -->
      <div class="footer-center">
        <div class="slogan">
          <h3>THE DIFFERENCE BETWEEN</h3>
          <h3>GOOD AND BAD</h3>
          <h3 class="highlight">ARCHITECTURE IS THE TIME YOU SPEND ON IT</h3>
        </div>
      </div>

      <!-- RIGHT SIDE: CONTACT -->
      <div class="footer-right">
        <h2>Contact</h2>
        <div
          class="contact-item"
          v-for="(phone, index) in phoneNumbers"
          :key="index"
        >
          <i class="fas fa-phone-alt contact-icon"></i>
          <a :href="`tel:${phone}`">{{ phone }}</a>
        </div>
      </div>
    </div>

    <!-- COPYRIGHT -->
    <div class="footer-bottom">
      <p>
        © {{ new Date().getFullYear() }} Mura Creatives — All Rights Reserved.
      </p>
    </div>
  </footer>
</template>

<script>
import logoWhite from "@/assets/mura-creatives-logo-white.png";
import logoBlack from "@/assets/mura-creatives-logo-black.png";

export default {
  name: "FooterSection",
  data() {
    return {
      themeMode: "light", // default theme
      phoneNumbers: ["+251947485789", "+251968414867"],
    };
  },
  computed: {
    logoSrc() {
      return this.themeMode === "dark" ? logoWhite : logoBlack;
    },
  },
  methods: {
    goToTelegram() {
      window.open("https://t.me/MuraCreatives", "_blank");
    },
    applyTheme(mode) {
      this.themeMode = mode;
      document.body.classList.toggle("dark", this.themeMode === "dark");
      localStorage.themeMode = this.themeMode;
    },
  },
  mounted() {
    const saved = localStorage.getItem("themeMode");
    if (saved) {
      this.applyTheme(saved);
    } else if (
      window.matchMedia &&
      window.matchMedia("(prefers-color-scheme: dark)").matches
    ) {
      this.applyTheme("dark");
    }
  },
};
</script>

<style scoped>
.footer-wrapper {
  z-index: 9999;
  background: rgba(255, 255, 255, 0.04);
  backdrop-filter: blur(20px);
  border-top: 1px solid rgba(255, 255, 255, 0.15);
  color: var(--text-color);
  padding: 60px 20px 30px;
  position: relative;
  overflow: hidden;
  font-family: "Poppins", sans-serif;
}

/* Decorative glowing gradient line */
.footer-wrapper::before {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  width: 120%;
  height: 2px;
  background: linear-gradient(90deg, #ff4e50, #f9d423, #ff4e50);
  transform: translateX(-50%);
  animation: moveGradient 6s linear infinite;
}

@keyframes moveGradient {
  from {
    background-position: 0%;
  }
  to {
    background-position: 100%;
  }
}

.footer-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 40px;
  align-items: start;
  justify-content: space-between;
}

.brand-logo-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.brand-logo {
  width: 120px;
  transition: transform 0.4s ease;
  filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.2));
}
.brand-logo:hover {
  transform: scale(1.1);
}

.telegram-subscribe {
  margin-top: 20px;
  text-align: left;
}
.telegram-subscribe p {
  font-size: 0.95rem;
  margin-bottom: 10px;
  color: var(--text-muted);
}
.telegram-btn {
  background: linear-gradient(135deg, #ff4e50, #f9d423);
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px 18px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}
.telegram-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 0 12px rgba(255, 78, 80, 0.6);
}

.slogan {
  text-align: center;
  color: var(--text-color);
}
.slogan h3 {
  margin: 3px 0;
  font-weight: 600;
  letter-spacing: 1px;
  font-size: 1rem;
}
.slogan .highlight {
  background: linear-gradient(90deg, #ff4e50, #f9d423);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 700;
  font-size: 1.1rem;
}

.footer-right h2 {
  margin-bottom: 15px;
  color: var(--primary-color);
  font-size: 1.4rem;
}
.contact-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.contact-icon {
  color: #f9d423;
  margin-right: 10px;
}
.contact-item a {
  text-decoration: none;
  color: var(--text-color);
  transition: color 0.3s ease;
}
.contact-item a:hover {
  color: #f9d423;
}

/* BOTTOM COPYRIGHT */
.footer-bottom {
  margin-top: 40px;
  text-align: center;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 15px;
  font-size: 0.85rem;
  color: var(--text-muted);
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .footer-container {
    text-align: center;
  }
  .brand-logo-container {
    justify-content: center;
  }
  .telegram-subscribe {
    text-align: center;
  }
  .telegram-btn {
    width: 100%;
  }
}
</style>
