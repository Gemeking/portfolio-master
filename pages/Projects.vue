<template>
  <div class="about page animate__animated animate__fadeIn">
    <h2>Recent Projects</h2>
    <div class="container">
      <div class="row align-items-center mb-5" v-for="(project, index) in projects" :key="index">
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
            <b-carousel-slide v-for="(image, imgIndex) in project.images" :key="imgIndex">
              <template #img>
                <img
                  class="d-block w-100 project-image"
                  :src="image"
                  :alt="`${project.title} image ${imgIndex + 1}`"
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
            <b-link v-if="project.link" :href="project.link" target="_blank" class="mr-3">
              Check it out! <LinkIcon style="color: #000;" />
            </b-link>
            <b-link v-if="project.github_url" :href="project.github_url" target="_blank">
              View source code <GithubIcon style="color: #000;" />
            </b-link>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LinkIcon from "vue-ionicons/dist/md-link.vue";
import GithubIcon from "vue-ionicons/dist/logo-github.vue";
import { BCarousel, BCarouselSlide } from "bootstrap-vue";

export default {
  components: {
    GithubIcon,
    LinkIcon,
    BCarousel,
    BCarouselSlide,
  },
  data() {
    return {
      projects: [
        {
          title: "Luxury Interior Design",
          category: "Interior Design",
          description: "Modern and luxurious interior design for residential and commercial spaces.",
          images: [
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLat8bZvhXD3ChSXyzGsFVh6qgplm1KhYPKA&s",
          ],
          github_url: "",
          link: "YOUR_PROJECT_LINK_HERE",
        },
        {
          title: "Brand Identity for Startup",
          category: "Graphic Design / Logo",
          description: "Crafting a unique brand identity including logos, business cards, and social media graphics.",
          images: [
            "YOUR_FIRST_IMAGE_URL_HERE",
            "YOUR_SECOND_IMAGE_URL_HERE",
            "YOUR_THIRD_IMAGE_URL_HERE",
          ],
          github_url: "",
          link: "YOUR_PROJECT_LINK_HERE",
        },
        {
          title: "Creative Office Space",
          category: "Interior Design",
          description: "Designing functional and aesthetic office spaces to enhance creativity and productivity.",
          images: [
            "YOUR_FIRST_IMAGE_URL_HERE",
            "YOUR_SECOND_IMAGE_URL_HERE",
            "YOUR_THIRD_IMAGE_URL_HERE",
          ],
          github_url: "",
          link: "YOUR_PROJECT_LINK_HERE",
        }
      ],
    };
  },
  head: {
    title: "Recent Projects 💻 - Architecture Designer",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Explore the recent interior, graphic design, and branding projects by a passionate architecture designer."
      },
      {
        hid: "og:title",
        name: "og:title",
        content: "Recent Projects 💻 - Architecture Designer"
      },
      {
        property: "og:description",
        content:
          "Explore the recent interior, graphic design, and branding projects by a passionate architecture designer."
      },
      {
        hid: "og:image",
        name: "og:image",
        content: "YOUR_DEFAULT_OG_IMAGE_URL"
      }
    ]
  }
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
  height: 400px; /* Adjust height as needed for consistency */
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
</style>