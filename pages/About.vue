<template>
  <div class="about-wrapper container animate__animated animate__fadeIn">
    <div class="row align-items-start gx-5 about-row">
      <!-- LEFT CONTENT -->
      <div class="col-md-6 about-left">
        <h1 class="title mb-3">About Me</h1>
        <h2 class="name mb-4">Architect Billionaire <span>Murad</span></h2>
        <p class="intro">
          I'm <b>Murad Mursela</b>, an <b>Architect</b> and <b>Graphic Designer</b>
          from Ethiopia, blending creativity and precision to design impactful
          spaces and visuals. My passion lies in turning ideas into
          architectural masterpieces and unforgettable brands.
        </p>

        <h3 class="section-title mt-4">In Architecture Design</h3>
        <ul class="custom-list">
          <li>Floor plan making and rendering</li>
          <li>3D modeling and rendering</li>
          <li>Facade design</li>
          <li>Animation videos</li>
          <li>Software setup</li>
          <li>Review drawings</li>
          <li>Supervise projects</li>
          <li>Interior design</li>
          <li>Material selection</li>
          <li>Material supply & allocation</li>
          <li>Furniture design</li>
          <li>Portfolio preparation</li>
        </ul>

        <h3 class="section-title mt-4">Our Services</h3>
        <div class="service-columns">
          <div class="service-block">
            <h5>Graphic Design</h5>
            <ul class="custom-list">
              <li>Logo Design</li>
              <li>T-Shirt & Poster Design</li>
              <li>Full Branding</li>
              <li>YouTube Thumbnail</li>
              <li>Banner & Sticker Design</li>
              <li>Ticket & Flyer Design</li>
              <li>Book Cover & Certificate</li>
              <li>Wedding Card Design</li>
            </ul>
          </div>
          <div class="service-block">
            <h5>Architectural Design</h5>
            <ul class="custom-list">
              <li>Floor Plan Creation & Rendering</li>
              <li>3D Modeling & Rendering</li>
              <li>Facade Design</li>
              <li>Animation Video Production</li>
              <li>Software Setup & Support</li>
              <li>Project Supervision</li>
              <li>Interior Design & Material Allocation</li>
              <li>Furniture & Portfolio Design</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- RIGHT SIDE - TOOLS (NOW AT TOP) -->
      <div class="col-md-6 about-right">
        <div class="tools-section">
          <h3 class="tools-title">Tools I Use</h3>
          <div class="tools-gallery">
            <div
              v-for="(tool, index) in tools"
              :key="index"
              class="tool-card"
              :style="{ animationDelay: `${index * 0.15}s` }"
            >
              <div class="tool-glow"></div>
              <img
                :src="`/tools/${tool.image}`"
                :alt="tool.name"
                class="tool-img"
              />
              <p class="tool-name">{{ tool.name }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutMurad",
  data() {
    return {
      tools: [
        { name: "Revit", image: "Revit.png" },
        { name: "AutoCAD", image: "AutoCAD.png" },
        { name: "SketchUp", image: "Sketchup.png" },
        { name: "Lumion", image: "Lumion.png" },
        { name: "Rhino", image: "Rhino.png" },
        { name: "D5 Render", image: "D5.png" },
        { name: "Photoshop", image: "Photoshop.png" },
        { name: "Illustrator", image: "illustrator.png" },
        { name: "InDesign", image: "Indesign.png" }
      ]
    };
  },
  head: {
    title: "About - Murad Mursela",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "Murad Mursela - Architect & Graphic Designer. Expert in 3D Design, Rendering, Branding, Logo Design, and Creative Architectural Projects using Revit, Lumion, Rhino, and Adobe tools."
      }
    ]
  }
};
</script>

<style scoped>
/* --- GENERAL LAYOUT --- */
.about-wrapper {
  margin-top: 6px;
  margin-bottom: 60px;
  color: var(--text-color);
  overflow: hidden;
}

.about-row {
  min-height: 80vh;
  display: flex;
  align-items: flex-start;
}

.about-left {
  padding-right: 2rem;
  animation: fadeInLeft 1.2s ease;
}

.title {
  font-size: 3rem;
  font-weight: 700;
  letter-spacing: 1px;
  position: relative;
  display: inline-block;
  margin-bottom: 0.5rem;
}

.title::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: -6px;
  width: 60%;
  height: 4px;
  background: linear-gradient(90deg, #ff4e50, #f9d423);
  border-radius: 4px;
}

.name {
  font-size: 2.2rem;
  font-weight: 600;
  margin-bottom: 1rem;
}
.name span {
  color: #d32e2e;
}

.intro {
  margin-top: 5px;
  font-size: 1.1rem;
  line-height: 1.9;
  margin-bottom: 1.2rem;
}

.section-title {
  color: #d32e2e;
  font-weight: 700;
  margin-bottom: 10px;
  font-size: 1.4rem;
}

.custom-list {
  list-style-type: "✦ ";
  padding-left: 25px;
  font-size: 1.05rem;
  line-height: 1.8;
}

/* --- SERVICE BLOCKS --- */
.service-columns {
  display: flex;
  flex-wrap: wrap;
  gap: 25px;
}
.service-block {
  flex: 1;
  min-width: 250px;
  background: rgba(255, 255, 255, 0.06);
  backdrop-filter: blur(8px);
  padding: 15px 20px;
  border-radius: 15px;
  transition: all 0.4s ease;
}
.service-block:hover {
  transform: translateY(-5px);
  background: rgba(255, 255, 255, 0.12);
}

/* --- TOOL SECTION --- */
.about-right {
  text-align: center;
  animation: fadeInRight 1.2s ease;
}

.tools-section {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(8px);
  border-radius: 20px;
  padding: 25px;
  margin-top: 15px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.tools-title {
  font-size: 2rem;
  font-weight: 700;
  color: #d32e2e;
  margin-bottom: 20px;
}

.tools-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 30px;
  justify-items: center;
}

.tool-card {
  position: relative;
  width: 120px;
  height: 130px;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 15px;
  padding: 15px;
  transition: transform 0.6s ease, box-shadow 0.6s ease;
  animation: floatUp 2.5s infinite ease-in-out;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}
.tool-card:hover {
  transform: scale(1.15) rotate(3deg);
  box-shadow: 0 12px 25px rgba(211, 46, 46, 0.3);
}

.tool-glow {
  position: absolute;
  top: -40%;
  left: -40%;
  width: 180%;
  height: 180%;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.12), transparent 70%);
  filter: blur(40px);
  z-index: 0;
  animation: rotateGlow 6s linear infinite;
}

.tool-img {
  width: 75px;
  height: 75px;
  object-fit: contain;
  filter: brightness(1.1);
  position: relative;
  z-index: 1;
  transition: transform 0.4s ease;
}
.tool-card:hover .tool-img {
  transform: scale(1.2) rotate(8deg);
}

.tool-name {
  margin-top: 10px;
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 0.5px;
  z-index: 1;
  position: relative;
}

/* --- ANIMATIONS --- */
@keyframes rotateGlow {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes floatUp {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-60px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(60px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* --- RESPONSIVE --- */
@media (max-width: 991px) {
  .about-row {
    flex-direction: column;
    align-items: center;
  }

  .about-left,
  .about-right {
    text-align: center;
    padding-right: 0;
  }

  .tools-section {
    margin-bottom: 30px;
  }

  .tools-gallery {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  }
}
</style>
