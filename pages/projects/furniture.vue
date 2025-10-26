<template>
  <div class="projects-page container animate__animated animate__fadeIn">
    <h2 class="page-title">Recent Projects</h2>
    <div
      class="project-row align-items-center mb-5"
      v-for="(project, index) in projects"
      :key="index"
    >
      <!-- IMAGE CAROUSEL -->
      <div class="col-md-6 project-carousel-wrapper">
        <b-carousel
          :id="'carousel-' + index"
          controls
          indicators
          background="transparent"
          img-width="1024"
          img-height="480"
          class="project-carousel"
          :interval="5000"
        >
          <b-carousel-slide
            v-for="(image, imgIndex) in project.images"
            :key="imgIndex"
          >
            <template #img>
              <img
                class="d-block w-100 project-image"
                :src="image"
                :alt="`${project.title} image ${imgIndex + 1}`"
                @click="openLightbox(project.images, imgIndex)"
                loading="lazy"
              />
            </template>
          </b-carousel-slide>
        </b-carousel>
      </div>

      <!-- PROJECT DETAILS -->
      <div class="col-md-6 project-details">
        <h2 class="project-title">{{ project.title }}</h2>
        <p class="category">{{ project.category }}</p>
        <hr class="highlight" />
        <b-card class="description-card text-left border-0">
          <p>{{ project.description }}</p>

          <div v-if="project.areas" class="areas-section">
            <h5>Featured Areas:</h5>
            <ul class="areas-list">
              <li v-for="(area, areaIndex) in project.areas" :key="areaIndex">
                {{ area }}
              </li>
            </ul>
          </div>

          <div class="action-buttons">
            <b-button
              variant="danger"
              @click="openGallery(project)"
              class="action-btn"
            >
              View {{ project.title }}
            </b-button>
            <b-link
              v-if="project.link"
              :href="project.link"
              target="_blank"
              class="link-btn"
            >
              Check it out! <LinkIcon />
            </b-link>
            <b-link
              v-if="project.github_url"
              :href="project.github_url"
              target="_blank"
              class="link-btn"
            >
              View source <GithubIcon />
            </b-link>
          </div>
        </b-card>
      </div>
    </div>

    <!-- GALLERY MODAL -->
    <b-modal
      v-model="showGallery"
      size="xl"
      centered
      hide-footer
      :title="selectedProject ? `${selectedProject.title} Gallery` : 'Gallery'"
      class="gallery-modal"
    >
      <div class="gallery-grid">
        <div
          v-for="(img, i) in selectedProjectImages"
          :key="i"
          class="gallery-item"
          @click="openLightbox(selectedProjectImages, i)"
        >
          <img
            :src="img"
            :alt="`${selectedProject ? selectedProject.title : 'Project'} - ${i + 1}`"
            loading="lazy"
          />
        </div>
      </div>
    </b-modal>

    <!-- LIGHTBOX -->
    <b-modal
      v-model="showLightbox"
      hide-header
      hide-footer
      centered
      size="xl"
      modal-class="lightbox-modal"
      body-class="p-0 bg-dark"
      content-class="border-0 rounded-0"
    >
      <div class="lightbox-arrow left" @click="prevImage">‹</div>
      <div class="lightbox-arrow right" @click="nextImage">›</div>
      <div class="lightbox-close" @click="showLightbox = false">&times;</div>
      <img
        :src="lightboxImages[lightboxIndex]"
        alt="Enlarged view"
        class="lightbox-img"
        loading="lazy"
      />
      <div class="lightbox-caption">
        Image {{ lightboxIndex + 1 }} of {{ lightboxImages.length }}
      </div>
    </b-modal>
  </div>
</template>

<script>
import LinkIcon from "vue-ionicons/dist/md-link.vue";
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import { BCarousel, BCarouselSlide, BModal, BButton, BLink } from "bootstrap-vue";

export default {
  components: { GithubIcon, LinkIcon, BCarousel, BCarouselSlide, BModal, BButton, BLink },
  data() {
    return {
      showGallery: false,
      selectedProjectImages: [],
      selectedProject: null,
      showLightbox: false,
      lightboxImages: [],
      lightboxIndex: 0,
      projects: [
        {
          title: "Kids Closet",
          category: "Interior Design Collection",
          description:
            "A stylish and functional kids closet design combining playful colors and smart storage for comfort and organization.",
          areas: ["Kids Room", "Closet Design", "Storage Optimization", "Playful Colors"],
          images: Array.from({ length: 5 }, (_, i) => `/kids/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Kitchen",
          category: "Modern Kitchen Interiors",
          description:
            "A versatile kitchen collection featuring terrace kitchens, main kitchens, and open kitchen designs that blend aesthetics with practicality.",
          areas: ["Terrace Kitchen", "Main Kitchen", "Open Kitchen", "Cabinet Design"],
          images: Array.from({ length: 9 }, (_, i) => `/kitchen/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Master Closet",
          category: "Luxury Closet Concepts",
          description:
            "Elegant and spacious master closet designs featuring functional layouts and refined finishes for a luxurious experience.",
          areas: ["Walk-in Closet", "Storage Design", "Lighting", "Luxury Finish"],
          images: Array.from({ length: 5 }, (_, i) => `/master/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "TV Stand",
          category: "Modern Living Space",
          description:
            "A showcase of contemporary TV stand designs that emphasize form, balance, and material harmony for modern interiors.",
          areas: ["Living Room", "Furniture Design", "Minimalist Layout", "Wood & Metal Fusion"],
          images: Array.from({ length: 4 }, (_, i) => `/tv/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
      ],
    };
  },
  methods: {
    openGallery(project) {
      this.selectedProjectImages = project.images;
      this.selectedProject = project;
      this.showGallery = true;
    },
    openLightbox(images, index) {
      this.lightboxImages = images;
      this.lightboxIndex = index;
      this.showLightbox = true;
    },
    prevImage() {
      if (this.lightboxImages.length === 0) return;
      this.lightboxIndex =
        (this.lightboxIndex - 1 + this.lightboxImages.length) % this.lightboxImages.length;
    },
    nextImage() {
      if (this.lightboxImages.length === 0) return;
      this.lightboxIndex = (this.lightboxIndex + 1) % this.lightboxImages.length;
    },
  },
  head: {
    title: "Interior Projects - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Explore Murad Mursela's interior projects, including kids closets, modern kitchens, luxury master closets, and contemporary TV stands, blending innovative design with functional aesthetics.",
      },
    ],
  },
};
</script>

<style scoped>
.projects-page {
  margin: 80px auto;
  max-width: 1200px;
  font-family: 'Poppins', sans-serif;
  color: var(--text-color, #ffffff);
  position: relative;
  z-index: 1;
}

.page-title {
  font-size: 3.5rem;
  font-weight: 800;
  background: linear-gradient(90deg, #ff4e50, #f9d423);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 50px;
  text-align: center;
  position: relative;
  animation: slideInDown 1.2s ease-out;
}

.page-title::after {
  content: "";
  position: absolute;
  left: 50%;
  bottom: -8px;
  transform: translateX(-50%);
  width: 100px;
  height: 5px;
  background: linear-gradient(90deg, #ff4e50, #f9d423);
  border-radius: 5px;
  transition: width 0.4s ease;
}

.page-title:hover::after {
  width: 150px;
}

.project-row {
  display: flex;
  align-items: stretch;
  background: linear-gradient(145deg, rgba(20, 20, 30, 0.9), rgba(40, 40, 50, 0.8));
  border-radius: 20px;
  padding: 30px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  animation: slideInUp 1.2s ease-out;
  margin-bottom: 80px;
}

.project-carousel-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.project-carousel {
  border-radius: 15px;
  overflow: hidden;
  max-width: 600px;
  width: 100%;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.project-image {
  border-radius: 15px;
  object-fit: cover;
  height: 400px;
  cursor: pointer;
  transition: transform 0.4s ease, box-shadow 0.4s ease;
  filter: brightness(var(--brightness, 1.1)) drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
}

.project-image:hover {
  transform: scale(1.08);
  box-shadow: 0 12px 30px rgba(255, 78, 80, 0.3);
}

.project-details {
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.project-title {
  font-size: 2.2rem;
  font-weight: 700;
  color: #ff4e50;
  margin-bottom: 0.5rem;
}

.category {
  font-size: 1.1rem;
  font-style: italic;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 10px;
}

.highlight {
  border: none;
  border-top: 4px solid #ff4e50;
  width: 100px;
  margin: 15px 0;
  transition: width 0.4s ease;
}

.project-details:hover .highlight {
  width: 150px;
}

.description-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px);
  border-radius: 15px;
  padding: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: transform 0.4s ease, box-shadow 0.4s ease;
}

.description-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 30px rgba(255, 78, 80, 0.25);
}

.description-card p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.9);
}

.areas-section h5 {
  font-size: 1.3rem;
  font-weight: 600;
  color: #f9d423;
  margin: 15px 0 10px;
}

.areas-list {
  list-style: none;
  padding: 0;
}

.areas-list li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 8px;
  font-size: 1.05rem;
  color: rgba(255, 255, 255, 0.85);
}

.areas-list li::before {
  content: "✦";
  position: absolute;
  left: 0;
  color: #ff4e50;
  font-weight: bold;
}

.action-buttons {
  margin-top: 20px;
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}

.action-btn {
  background: linear-gradient(90deg, #ff4e50, #f9d423);
  border: none;
  padding: 10px 20px;
  font-weight: 600;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.action-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 20px rgba(255, 78, 80, 0.3);
}

.link-btn {
  font-weight: 500;
  color: #f9d423;
  display: flex;
  align-items: center;
  gap: 5px;
  transition: color 0.3s ease;
}

.link-btn:hover {
  color: #ff4e50;
  text-decoration: none;
}

.link-btn svg {
  fill: #f9d423;
  transition: fill 0.3s ease;
}

.link-btn:hover svg {
  fill: #ff4e50;
}

.gallery-modal .modal-dialog {
  max-width: 90%;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
}

.gallery-item img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 12px;
  cursor: pointer;
  transition: transform 0.4s ease, box-shadow 0.4s ease;
  filter: brightness(var(--brightness, 1.1));
}

.gallery-item img:hover {
  transform: scale(1.06);
  box-shadow: 0 10px 25px rgba(255, 78, 80, 0.3);
}

.lightbox-img {
  max-width: 90vw;
  max-height: 80vh;
  object-fit: contain;
  border-radius: 10px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
  filter: brightness(var(--brightness, 1.1));
}

.lightbox-arrow {
  position: absolute;
  top: 50%;
  font-size: 4rem;
  color: rgba(255, 255, 255, 0.8);
  cursor: pointer;
  transition: opacity 0.3s ease, transform 0.3s ease;
  transform: translateY(-50%);
  user-select: none;
}

.lightbox-arrow.left { left: 20px; }
.lightbox-arrow.right { right: 20px; }
.lightbox-arrow:hover {
  opacity: 1;
  transform: translateY(-50%) scale(1.1);
}

.lightbox-close {
  position: absolute;
  top: 20px;
  right: 30px;
  font-size: 2.8rem;
  color: rgba(255, 255, 255, 0.8);
  cursor: pointer;
  transition: opacity 0.3s ease, transform 0.3s ease;
  user-select: none;
}

.lightbox-close:hover {
  opacity: 1;
  transform: scale(1.1);
}

.lightbox-caption {
  margin-top: 15px;
  color: rgba(255, 255, 255, 0.9);
  font-weight: 500;
  text-align: center;
  font-size: 1.1rem;
}

/* --- ANIMATIONS --- */
@keyframes slideInDown {
  from {
    opacity: 0;
    transform: translateY(-60px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(60px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* --- RESPONSIVE --- */
@media (max-width: 991px) {
  .project-row {
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }

  .project-carousel-wrapper,
  .project-details {
    width: 100%;
    max-width: 100%;
  }

  .project-image {
    height: 300px;
  }

  .page-title {
    font-size: 2.8rem;
  }

  .project-title {
    font-size: 1.8rem;
  }
}

@media (max-width: 576px) {
  .project-image {
    height: 250px;
  }

  .gallery-item img {
    height: 150px;
  }

  .page-title {
    font-size: 2.2rem;
  }

  .project-title {
    font-size: 1.6rem;
  }

  .action-buttons {
    flex-direction: column;
    align-items: center;
  }

  .link-btn {
    margin-top: 10px;
  }
}
</style>