<template>
  <div class="cv-wrapper container animate__animated animate__fadeIn">
    <div class="row">
      <!-- LEFT: CV CONTENT -->
      <div class="col-lg-6 col-md-12">
        <div class="cv-content">
          <h1 class="cv-title">My Credentials</h1>
          <h4 class="cv-subtitle">Explore My Professional Achievements 👋</h4>
          <p class="cv-intro">
            Discover my professional credentials, certifications, and experiences as an architect and graphic designer. Each document can be downloaded to showcase my skills and achievements.
          </p>

          <h4 class="cv-doc-title mt-5">Documents & Certifications</h4>
          <p>Click on any item below to download the PDF:</p>

          <div class="credential-list">
            <div v-for="(credential, index) in credentials" :key="index" class="credential-card">
              <a :href="credential.path" :download="credential.name" class="credential-link">
                <div class="icon-box">
                  <i :class="credential.icon"></i>
                </div>
                <div class="details-box">
                  <h5>{{ credential.name }}</h5>
                  <p>{{ credential.description }}</p>
                </div>
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- RIGHT: IMAGE -->
      <div class="col-lg-6 col-md-12 text-center">
        <img src="@/assets/c.jpg" alt="Credentials Illustration" class="cv-image" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      credentials: [
        {
          name: "BSc Degree in Architecture",
          path: "/pdfs/BSCDegreeofArchitecture.pdf",
          description: "Official degree certificate from Wachemo University, Ethiopia.",
          icon: "fas fa-graduation-cap"
        },
        {
          name: "Work Experience Letter",
          path: "/pdfs/IMG_9198.JPG",
          description: "Professional experience in architecture and design.",
          icon: "fas fa-briefcase"
        },
        {
          name: "Exhibition Certificate",
          path: "/pdfs/exhibition.pdf",
          description: "Participation certificate in architecture & design exhibitions.",
          icon: "fas fa-palette"
        },
        {
          name: "Netherlands Certificate",
          path: "/pdfs/NetherlandCertificate.pdf",
          description: "Certification earned from a program in the Netherlands.",
          icon: "fas fa-certificate"
        },
        {
          name: "Recommendation Letter",
          path: "/pdfs/Recommendation 1.pdf",
          description: "Professional recommendation highlighting my skills.",
          icon: "fas fa-file-alt"
        },
        {
          name: "Dereja Certificate",
          path: "/pdfs/Dereja.pdf",
          description: "Certificate from the Dereja program for professional development.",
          icon: "fas fa-award"
        }
      ]
    };
  },
  head: {
    title: "CV 📜 - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content: "Explore Murad Mursela's professional credentials and certifications. Download BSc Degree, recommendation letters, and certificates."
      }
    ]
  }
};
</script>

<style scoped>
.cv-wrapper {
  margin-top: 120px;
  margin-bottom: 60px;
  color: var(--text-color);
  font-family: 'Poppins', sans-serif;
}

/* --- TITLES --- */
.cv-title {
  font-size: 2.8rem;
  font-weight: 700;
  color: var(--primary-color);
  position: relative;
  display: inline-block;
  margin-bottom: 0.8rem;
}
.cv-title::after {
  content: '';
  position: absolute;
  bottom: -8px;
  left: 0;
  width: 60px;
  height: 4px;
  border-radius: 3px;
  background: linear-gradient(90deg, #ff4e50, #f9d423);
}

.cv-subtitle {
  font-size: 1.2rem;
  color: var(--text-muted);
  margin-bottom: 20px;
}

.cv-intro {
  line-height: 1.8;
  color: var(--text-muted);
}

/* --- CREDENTIAL CARDS --- */
.credential-list {
  display: grid;
  grid-template-columns: 1fr;
  gap: 15px;
  margin-top: 20px;
}

.credential-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(12px);
  border-radius: 15px;
  transition: all 0.4s ease;
  overflow: hidden;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
}
.credential-card:hover {
  transform: translateY(-6px) scale(1.02);
  box-shadow: 0 12px 30px rgba(211, 46, 46, 0.35);
}

.credential-link {
  display: flex;
  align-items: flex-start;
  padding: 15px;
  text-decoration: none;
  color: var(--text-color);
}

.icon-box {
  flex-shrink: 0;
  width: 55px;
  height: 55px;
  background: var(--primary-color);
  color: #fff;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  margin-right: 15px;
  transition: transform 0.4s ease;
}
.credential-card:hover .icon-box {
  transform: rotate(15deg) scale(1.1);
}

.details-box h5 {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 600;
}
.details-box p {
  margin: 5px 0 0;
  font-size: 0.9rem;
  color: var(--text-muted);
}

/* --- IMAGE --- */
.cv-image {
  width: 100%;
  max-width: 400px;
  border-radius: 15px;
  box-shadow: 0 12px 28px rgba(0,0,0,0.15);
  transition: transform 0.4s ease, box-shadow 0.4s ease;
}
.cv-image:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 20px 40px rgba(211,46,46,0.3);
}

/* --- RESPONSIVE --- */
@media (max-width: 991px) {
  .cv-wrapper {
    text-align: center;
  }
  .credential-link {
    flex-direction: column;
    align-items: center;
  }
  .icon-box {
    margin-bottom: 10px;
  }
}
</style>
