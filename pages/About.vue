<template>
  <div class="about-wrapper container animate__animated animate__fadeIn">
    <!-- ✅ ENHANCED TOOLS SECTION (TOP-RIGHT CORNER) -->
    <div class="tools-fixed-top-right">
      <h3 class="tools-title">Tools I Use</h3>
      <div class="tools-gallery">
        <div
          v-for="(tool, index) in tools"
          :key="index"
          class="tool-card"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div class="tool-glow"></div>
          <img :src="`/tools/${tool.image}`" :alt="tool.name" class="tool-img" />
          <p class="tool-name">{{ tool.name }}</p>
        </div>
      </div>
    </div>

    <!-- ✅ ABOUT SECTION -->
    <div class="row align-items-start gx-5 about-row">
      <div class="col-lg-6 about-left">
        <div class="profile-wrapper">
          <div class="photo-frame">
            <img src="@/assets/murad.png" alt="Murad Mursela" class="profile-photo" />
            <div class="photo-glow"></div>
          </div>
          <div class="name-section">
            <h1 class="title">About Me</h1>
            <h2 class="name"><span>Murad</span> Mursela</h2>
            <p class="intro">
              I'm <b>Murad Mursela</b>, an <b>Architect</b> and <b>Graphic Designer</b>
              from Ethiopia — blending creativity and precision to design impactful
              spaces and visuals. I turn bold ideas into architectural masterpieces and
              unforgettable brands.
            </p>
          </div>
        </div>

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
  mounted() {
    // Add interactive effects
    const toolCards = document.querySelectorAll('.tool-card');
    
    toolCards.forEach(card => {
      card.addEventListener('mouseenter', function() {
        this.style.zIndex = '10';
      });
      
      card.addEventListener('mouseleave', function() {
        this.style.zIndex = '1';
      });
    });
  }
};
</script>

<style scoped>
.about-wrapper {
  margin-top: 40px;
  margin-bottom: 60px;
  color: var(--text-color);
  overflow: hidden;
  position: relative;
}

/* ✅ Enhanced Fixed top-right tools section */
.tools-fixed-top-right {
  position: fixed;
  top: 90px;
  right: 90px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 20px;
  padding: 25px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  z-index: 1000;
  width: 480px;
  height:560px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.4s ease;
}

.tools-fixed-top-right:hover {
  background: rgba(255, 255, 255, 0.12);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
  transform: translateY(-5px);
}

.tools-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ff6b6b;
  margin-bottom: 25px;
  text-align: center;
  position: relative;
  padding-bottom: 12px;
}

.tools-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background: linear-gradient(90deg, #ff6b6b, #ffd166);
  border-radius: 3px;
}

.tools-gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
  justify-items: center;
}

/* --- ENHANCED TOOL CARD --- */
.tool-card {
  position: relative;
  width: 100px;
  height: 120px;
  background: linear-gradient(135deg, rgba(255, 107, 107, 0.1) 0%, rgba(255, 209, 102, 0.1) 100%);
  border-radius: 16px;
  padding: 15px;
  transition: all 0.4s ease;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(255, 255, 255, 0.05);
  cursor: pointer;
  animation: floatUp 3s infinite ease-in-out;
}

.tool-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
}

.tool-card:hover {
  transform: translateY(-8px) scale(1.05);
  background: linear-gradient(135deg, rgba(255, 107, 107, 0.2) 0%, rgba(255, 209, 102, 0.2) 100%);
  box-shadow: 0 12px 25px rgba(255, 107, 107, 0.3);
}

.tool-glow {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 16px;
  background: radial-gradient(circle at center, rgba(255, 107, 107, 0.2) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.tool-card:hover .tool-glow {
  opacity: 1;
}

.tool-img {
  width: 50px;
  height: 50px;
  object-fit: contain;
  z-index: 1;
  transition: all 0.4s ease;
  filter: drop-shadow(0 0 8px rgba(255, 107, 107, 0.4));
}

.tool-card:hover .tool-img {
  transform: scale(1.2) rotate(5deg);
  filter: drop-shadow(0 0 12px rgba(255, 107, 107, 0.7));
}

.tool-name {
  margin-top: 12px;
  font-weight: 600;
  font-size: 0.85rem;
  color: #ffd166;
  text-align: center;
  z-index: 1;
  transition: all 0.3s ease;
}

.tool-card:hover .tool-name {
  color: #ff9e6d;
  transform: translateY(2px);
}

/* --- FLOAT ANIMATION --- */
@keyframes floatUp {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

/* --- ABOUT SECTION --- */
.about-row {
  display: flex;
  align-items: flex-start;
}

.about-left {
  animation: fadeInLeft 1.2s ease;
}

.profile-wrapper {
  display: flex;
  align-items: center;
  gap: 40px;
  flex-wrap: wrap;
  margin-bottom: 30px;
  justify-content: flex-start;
}

.photo-frame {
  position: relative;
  overflow: hidden;
  border-radius: 20px;
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.25);
  transition: transform 0.4s ease;
}

.profile-photo {
  width: 100%;
  max-height: 620px;
  object-fit: contain;
  display: block;
  transition: transform 0.5s ease;
}

.photo-frame:hover .profile-photo {
  transform: scale(1.05);
}

.name-section { flex: 1; text-align: left; }

.title {
  font-size: 2.8rem;
  font-weight: 700;
  position: relative;
  margin-bottom: 0.4rem;
}
.title::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: -6px;
  width: 70%;
  height: 4px;
  background: linear-gradient(90deg, #ff6b6b, #ffd166);
  border-radius: 4px;
}

.name { font-size: 2.2rem; font-weight: 600; }
.name span { color: #ff6b6b; }

.intro {
  margin-top: 10px;
  font-size: 1.1rem;
  line-height: 1.8;
  margin-bottom: 1rem;
}

/* --- SERVICES --- */
.section-title { 
  color: #ff6b6b; 
  font-weight: 700; 
  margin-bottom: 10px; 
  font-size: 1.4rem; 
}

.service-columns { display: flex; flex-wrap: wrap; gap: 20px; }

.service-block {
  flex: 1;
  min-width: 250px;
  background: rgba(255, 255, 255, 0.06);
  backdrop-filter: blur(8px);
  padding: 18px 20px;
  border-radius: 16px;
  transition: all 0.4s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
}
.service-block:hover {
  transform: translateY(-6px) scale(1.02);
  background: rgba(255, 255, 255, 0.12);
  box-shadow: 0 8px 25px rgba(255, 107, 107, 0.3);
}

.custom-list {
  list-style-type: "✦ ";
  padding-left: 25px;
  font-size: 1rem;
  line-height: 1.8;
}

/* --- RESPONSIVE --- */
@media (max-width: 991px) {
  .tools-fixed-top-right {
    position: relative;
    width: 100%;
    max-width: 500px;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    background: rgba(255, 255, 255, 0.9);
    margin: 0 auto 30px;
    top: 60px;
    right: auto;
  }
  .photo-frame {
    display:none;
  }
  
  .tools-gallery {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  }
}

@media (max-width: 480px) {
  .tools-fixed-top-right {
    padding: 20px 15px;
  }
  
  .tools-gallery {
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
  }
  
  .tool-card {
    width: 85px;
    height: 100px;
    padding: 12px;
  }
  
  .tool-img {
    width: 40px;
    height: 40px;
  }
  
  .tool-name {
    font-size: 0.75rem;
  }
}
</style>