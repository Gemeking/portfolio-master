<template>
  <div class="container animate__animated animate__fadeIn">
    <div class="row">
      <div class="col-md-6">
        <div class="cv-content">
          <h1 class="line-after">My Credentials</h1>
          <h4 class="mt-4">Explore My Qualifications 👋</h4>
          <p>
            Below is a collection of my professional credentials, certifications, and experiences as an architect and graphic designer. Each document is available for download to showcase my expertise and achievements.
          </p>
          <h4 class="mt-5">Documents & Certifications</h4>
          <p>Click on any item below to download the respective PDF document:</p>
          <div class="credential-list animate__animated animate__fadeInUp">
            <div v-for="(credential, index) in credentials" :key="index" class="credential-item">
              <a :href="credential.path" :download="credential.name" class="credential-link">
                <i :class="credential.icon" class="credential-icon"></i>
                <div class="credential-details">
                  <h5>{{ credential.name }}</h5>
                  <p>{{ credential.description }}</p>
                </div>
              </a>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <img
          src="@/assets/c.jpg"
          alt="Credentials Illustration"
          class="cv-img"
        />
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
          path: "/static/pdfs/BSC Degree of Architecture.pdf",
          description: "Official degree certificate from Wachemo University, Ethiopia.",
          icon: "fas fa-graduation-cap"
        },
        {
          name: "Work Experience Letter",
          path: "/static/pdfs/work-experience.pdf",
          description: "Documentation of my professional experience in architecture and design.",
          icon: "fas fa-briefcase"
        },
        {
          name: "Exhibition Certificate",
          path: "/static/pdfs/exhibition.pdf",
          description: "Certificate for participation in architectural and design exhibitions.",
          icon: "fas fa-palette"
        },
        {
          name: "Netherlands Certificate",
          path: "/static/pdfs/Netherland Certificate (2).pdf",
          description: "Certification earned from a program in the Netherlands.",
          icon: "fas fa-certificate"
        },
        {
          name: "Recommendation Letter",
          path: "/static/pdfs/Recommendation 1.pdf",
          description: "Professional recommendation highlighting my skills and work ethic.",
          icon: "fas fa-file-alt"
        },
        {
          name: "Dereja Certificate",
          path: "/static/pdfs/Dereja.pdf",
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
        content:
          "Explore the professional credentials of Murad Mursela, an architect and graphic designer from Ethiopia. Download my BSc Degree, certifications, and recommendation letters."
      }
    ],
    link: [
      {
        rel: "stylesheet",
        href: "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css",
        integrity: "sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw==",
        crossorigin: "anonymous"
      }
    ]
  }
};
</script>

<style scoped>
.container {
  margin-top: 140px;
  text-align: left;
  padding: 0 15px;
}

.line-after {
  overflow: hidden;
  color: #333;
  font-weight: 700;
}

.line-after::after {
  content: "";
  display: inline-block;
  height: 0.5em;
  vertical-align: bottom;
  width: 100%;
  margin-right: -100%;
  margin-left: 10px;
  border-top: 2px solid rgb(211, 46, 46);
}

.cv-content h4 {
  color: #444;
  font-weight: 600;
}

.cv-content p {
  color: #666;
  line-height: 1.6;
}

.credential-list {
  margin-top: 20px;
}

.credential-item {
  margin-bottom: 15px;
  padding: 15px;
  background: #f8f9fa;
  border-radius: 8px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.credential-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.credential-link {
  display: flex;
  align-items: center;
  text-decoration: none;
  color: #333;
}

.credential-icon {
  font-size: 24px;
  color: rgb(211, 46, 46);
  margin-right: 15px;
}

.credential-details h5 {
  margin: 0;
  font-size: 18px;
  font-weight: 600;
  color: #333;
}

.credential-details p {
  margin: 5px 0 0;
  font-size: 14px;
  color: #777;
}

.cv-img {
  width: 100%;
  height: auto;
  border-radius: 5px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
  .cv-img {
    margin-top: 20px;
  }
  .credential-item {
    padding: 10px;
  }
}
</style>