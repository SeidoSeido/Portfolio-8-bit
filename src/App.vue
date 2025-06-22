<template>
  <div id="app" @mousemove="updateSpotlight" ref="app">
    <div class="spotlight" :style="spotlightStyle"></div>
    <Navigation />
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    HeroSection,
    AboutSection,
    SkillsSection,
    ProjectsSection,
    ContactSection
  },
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
      isMouseMoving: false,
      fadeTimeout: null
    }
  },
  computed: {
    spotlightStyle() {
      return {
        left: this.mouseX + 'px',
        top: this.mouseY + 'px',
        opacity: this.isMouseMoving ? 0.8 : 0
      }
    }
  },
  methods: {
    updateSpotlight(event) {
      this.mouseX = event.clientX
      this.mouseY = event.clientY
      this.isMouseMoving = true
      
      // Clear existing timeout
      if (this.fadeTimeout) {
        clearTimeout(this.fadeTimeout)
      }
      
      // Fade out after mouse stops moving
      this.fadeTimeout = setTimeout(() => {
        this.isMouseMoving = false
      }, 100)
    }
  },
  mounted() {
    // Initialize spotlight at center
    this.mouseX = window.innerWidth / 2
    this.mouseY = window.innerHeight / 2
  },
  beforeUnmount() {
    if (this.fadeTimeout) {
      clearTimeout(this.fadeTimeout)
    }
  }
}
</script>

<style>
#app {
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}

.spotlight {
  position: fixed;
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 0.1) 0%,
    rgba(255, 255, 255, 0.05) 30%,
    rgba(255, 255, 255, 0.02) 60%,
    transparent 100%
  );
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
  transition: opacity 0.3s ease;
  mix-blend-mode: screen;
}

/* Enhanced spotlight on hover areas */
.spotlight::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 0.15) 0%,
    rgba(255, 255, 255, 0.08) 50%,
    transparent 100%
  );
  transform: translate(-50%, -50%);
}

/* Pulse effect for interactive elements */
.btn:hover,
.project-card:hover,
.skill-item:hover,
.info-card:hover {
  box-shadow: 
    0 0 20px rgba(255, 255, 255, 0.1),
    0 0 40px rgba(255, 255, 255, 0.05);
}

/* Enhanced glow for game area */
.game-board:hover {
  box-shadow: 
    0 0 30px rgba(0, 255, 0, 0.2),
    inset 0 0 30px rgba(0, 255, 0, 0.1);
}

/* Subtle glow on navigation links */
.nav-links a:hover {
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
}

/* Code animation glow effect */
.code-animation:hover {
  box-shadow: 
    0 0 20px rgba(0, 255, 0, 0.3),
    inset 0 0 20px rgba(0, 255, 0, 0.1);
}
</style>
