<template>
  <div class="about page animate__animated animate__fadeIn">
    <h2>Recent Projects</h2>
    <div class="container">
      <div
        class="row align-items-center mb-5"
        v-for="(project, index) in projects"
        :key="index"
      >
        <div class="col-md-6">
          <b-carousel
            :id="'carousel-' + index"
            controls
            indicators
            background="#ffffff"
            img-width="1024"
            img-height="480"
            class="project-carousel"
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
                />
              </template>
            </b-carousel-slide>
          </b-carousel>
        </div>

        <div class="col-md-6">
          <h2 class="mt-3 mb-0" style="text-align: left;">
            {{ project.title }}
          </h2>
          <p class="text-muted mb-3">{{ project.category }}</p>
          <hr class="dope" />
          <b-card class="mt-3 mb-3 text-left text-dark border-0 shadow-sm">
            <p>{{ project.description }}</p>

            <div v-if="project.areas" class="areas-section">
              <h5 class="mb-2">Featured Areas:</h5>
              <ul class="areas-list">
                <li v-for="(area, areaIndex) in project.areas" :key="areaIndex">
                  {{ area }}
                </li>
              </ul>
            </div>

            <b-button
              variant="danger"
              @click="openGallery(project)"
              class="mb-2"
            >
              View {{ project.title }}
            </b-button>

            <div>
              <b-link
                v-if="project.link"
                :href="project.link"
                target="_blank"
                class="mr-3"
              >
                Check it out! <LinkIcon style="color: #000;" />
              </b-link>
              <b-link
                v-if="project.github_url"
                :href="project.github_url"
                target="_blank"
              >
                View source code <GithubIcon style="color: #000;" />
              </b-link>
            </div>
          </b-card>
        </div>
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
          />
        </div>
      </div>
    </b-modal>

    <!-- LIGHTBOX VIEW -->
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
      />

      <div class="lightbox-caption text-white">
        Image {{ lightboxIndex + 1 }} of {{ lightboxImages.length }}
      </div>
    </b-modal>
  </div>
</template>

<script>
import LinkIcon from "vue-ionicons/dist/md-link.vue";
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import { BCarousel, BCarouselSlide, BModal, BButton } from "bootstrap-vue";

export default {
  components: { GithubIcon, LinkIcon, BCarousel, BCarouselSlide, BModal, BButton },
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
          title: "Apartment",
          category: "Architectural Design",
          description:
            "A modern apartment design collection showcasing creative layouts, spatial harmony, and aesthetic simplicity with strong architectural principles.",
          areas: ["Modern", "Minimal", "Urban Living", "Interior Planning", "3D Visualization"],
          images: Array.from({ length: 9 }, (_, i) => `/apartment/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Bank",
          category: "Corporate Building Design",
          description:
            "Concept designs for a professional and secure banking facility that blends functionality with modern architectural form.",
          areas: ["Corporate", "Facade Design", "Commercial Space", "3D Modeling", "Rendering"],
          images: Array.from({ length: 5 }, (_, i) => `/bank/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Hospital",
          category: "Health Facility Design",
          description:
            "Comprehensive hospital design project focusing on patient comfort, efficient circulation, and sustainable architectural solutions.",
          areas: ["Healthcare", "Architecture", "Interior Design", "Sustainability", "Planning"],
          images: Array.from({ length: 10 }, (_, i) => `/hospital/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Quick Design",
          category: "Concept & Poster Design",
          description:
            "Fast concept visualization and poster-style renderings that highlight architectural storytelling through digital art.",
          areas: ["Typography", "Concept Art", "Visualization", "Creative Layouts"],
          images: Array.from({ length: 13 }, (_, i) => `/quickdesign/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Acoustical Hall Design",
          category: "Cultural & Interior Design",
          description:
            "An acoustically optimized hall design project combining sound engineering principles with elegant architectural detailing.",
          areas: ["Interior Design", "Acoustics", "Lighting", "3D Visualization"],
          images: Array.from({ length: 15 }, (_, i) => `/hall/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Resort",
          category: "Hospitality Design",
          description:
            "A coastal resort project emphasizing comfort, natural aesthetics, and harmony between architecture and landscape.",
          areas: ["Resort", "Landscape Design", "Luxury Spaces", "Visualization"],
          images: Array.from({ length: 6 }, (_, i) => `/resort/${i + 1}.JPG`),
          github_url: "",
          link: "",
        },
        {
          title: "Studio",
          category: "Creative Workspaces",
          description:
            "A studio design emphasizing functionality, lighting balance, and creative atmosphere tailored for modern professionals.",
          areas: ["Workspaces", "Minimal Design", "Interior Planning"],
          images: Array.from({ length: 2 }, (_, i) => `/studio/${i + 1}.JPG`),
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
        (this.lightboxIndex - 1 + this.lightboxImages.length) %
        this.lightboxImages.length;
    },
    nextImage() {
      if (this.lightboxImages.length === 0) return;
      this.lightboxIndex =
        (this.lightboxIndex + 1) % this.lightboxImages.length;
    },
  },
  head: {
    title: "Projects",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Explore architectural and interior design works including apartments, hospitals, resorts, studios, and cultural spaces, blending creativity with functional design.",
      },
    ],
  },
};
</script>

<style scoped>
.row {
  margin-top: 70px;
}
.project-carousel {
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
.project-image {
  border-radius: 10px;
  object-fit: cover;
  height: 400px;
  cursor: pointer;
  transition: opacity 0.3s ease;
}
.project-image:hover {
  opacity: 0.92;
}
hr.dope {
  border: 0;
  width: 90px;
  border-top: 2px solid #dc3545;
  text-align: left;
  margin: 10px 0;
  margin-left: 0;
}
.text-muted {
  font-size: 1rem;
  font-style: italic;
}
.shadow-sm {
  transition: box-shadow 0.3s ease;
}
.shadow-sm:hover {
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}
.areas-section {
  margin-top: 15px;
}
.areas-section h5 {
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
}
.areas-list {
  list-style: none;
  padding: 0;
}
.areas-list li {
  font-size: 1rem;
  color: #444;
  margin-bottom: 8px;
  position: relative;
  padding-left: 20px;
}
.areas-list li::before {
  content: "•";
  position: absolute;
  left: 0;
  color: #dc3545;
  font-size: 1.4rem;
  line-height: 1rem;
}
.gallery-modal .modal-dialog {
  max-width: 90%;
}
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-gap: 15px;
}
.gallery-item {
  cursor: pointer;
}
.gallery-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 12px;
  transition: transform 0.3s ease;
}
.gallery-item img:hover {
  transform: scale(1.05);
}
.lightbox-modal .modal-content {
  background: #000;
  border: none;
  height: 98vh;
  border-radius: 0;
}
.lightbox-img {
  max-width: 92vw;
  max-height: 78vh;
  object-fit: contain;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.45);
}
.lightbox-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 3.8rem;
  color: #fff;
  cursor: pointer;
  opacity: 0.65;
  user-select: none;
  transition: opacity 0.25s ease;
}
.lightbox-arrow:hover {
  opacity: 1;
}
.lightbox-arrow.left {
  left: 18px;
}
.lightbox-arrow.right {
  right: 18px;
}
.lightbox-close {
  position: absolute;
  top: 18px;
  right: 28px;
  font-size: 2.6rem;
  color: #fff;
  cursor: pointer;
  opacity: 0.65;
  transition: opacity 0.25s ease;
  user-select: none;
}
.lightbox-close:hover {
  opacity: 1;
}
.lightbox-caption {
  margin-top: 12px;
  font-size: 1.15rem;
  font-weight: 500;
  letter-spacing: 0.5px;
}
</style>
