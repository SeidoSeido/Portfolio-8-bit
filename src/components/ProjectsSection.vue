<template>
  <section id="projects" class="projects section">
    <div class="container">      <div class="section-header" ref="sectionHeader">
        <h2 class="section-title pixel-title pixel-matrix-in">
          <span class="glitch-char">F</span><span class="glitch-char">E</span><span class="glitch-char">A</span><span class="glitch-char">T</span><span class="glitch-char">U</span><span class="glitch-char">R</span><span class="glitch-char">E</span><span class="glitch-char">D</span>
          <span class="space">&nbsp;</span>
          <span class="glitch-char">P</span><span class="glitch-char">R</span><span class="glitch-char">O</span><span class="glitch-char">J</span><span class="glitch-char">E</span><span class="glitch-char">C</span><span class="glitch-char">T</span><span class="glitch-char">S</span>
        </h2>
        <div class="section-line pixel-line pixel-expand"></div>
        <p class="section-description pixel-text pixel-fade-up">
          <span class="glitch-word">A</span> <span class="glitch-word">showcase</span> <span class="glitch-word">of</span> <span class="glitch-word">my</span> <span class="glitch-word">recent</span> <span class="glitch-word">work</span> <span class="glitch-word">and</span> <span class="glitch-word">creative</span> <span class="glitch-word">solutions</span>
        </p>
      </div>
      
      <div class="projects-filter pixel-filter-slide" ref="projectsFilter">
        <button 
          v-for="category in categories" 
          :key="category"
          @click="filterProjects(category)"
          :class="['filter-btn pixel-filter-btn', { active: activeFilter === category }]"
        >
          {{ category }}
        </button>
      </div>      <div class="projects-grid pixel-grid-container" ref="projectsGrid">
        <div 
          v-for="project in filteredProjects" 
          :key="project.id"
          class="project-card pixel-project-card"
          @mouseenter="project.isHovered = true"
          @mouseleave="project.isHovered = false"
        ><div class="project-image">
            <div class="project-placeholder" :style="{ background: project.color }">
              <div class="project-icon">
                <i :class="project.icon"></i>
              </div>
            </div>
            <div class="project-overlay" :class="{ visible: project.isHovered }">              <div class="project-links">
                <a href="#" class="project-link" title="View Live">
                  <i class="pixelart-icons-font-external-link"></i>
                </a>
                <a href="#" class="project-link" title="View Code">
                  <i class="pixelart-icons-font-github"></i>
                </a>
              </div>
            </div>
          </div>
            <div class="project-content">
            <div class="project-meta">
              <div class="project-category">{{ project.category }}</div>
              <div class="project-year">{{ project.year }}</div>
            </div>
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-role">
              <span class="role-label">Role:</span>
              <span class="role-text">{{ project.role }}</span>
            </div>
            
            <div class="project-tech">
              <span 
                v-for="tech in project.technologies" 
                :key="tech"
                class="tech-tag"
              >
                {{ tech }}
              </span>
            </div>              <div class="project-stats">
              <div class="stat">
                <i class="pixelart-icons-font-heart stat-icon"></i>
                <span>{{ project.stars }}</span>
              </div>
              <div class="stat">
                <i class="pixelart-icons-font-eye stat-icon"></i>
                <span>{{ project.views }}</span>            </div>          </div>
        </div>
      </div>
      </div>
      
      <div class="projects-cta">
        <p>Want to see more projects?</p>
        <a href="#" class="btn btn-primary">View All Projects</a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',
  data() {
    return {
      observer: null,
      activeFilter: 'All',      categories: ['All', 'AI/ML', 'Websites', 'E-commerce', 'DevSecOps', 'Mapping Systems'],
      projects: [
        {
          id: 1,
          title: 'AI-Powered Curriculum Evaluation and Alignment Platform',
          description: 'Advanced platform for evaluating and aligning educational curricula using artificial intelligence and machine learning algorithms.',
          category: 'AI/ML',
          technologies: ['Python', 'TensorFlow', 'Vue.js', 'FastAPI'],
          color: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
          icon: 'pixelart-icons-font-analytics',
          stars: 124,
          views: '2.1k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer, UI/UX Designer, Project Manager'
        },
        {
          id: 2,
          title: 'Campus eCommerce Platform for LPU Cavite Students',
          description: 'Comprehensive e-commerce platform designed specifically for LPU Cavite students with integrated payment systems and campus-specific features.',
          category: 'E-commerce',
          technologies: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe'],
          color: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
          icon: 'pixelart-icons-font-shopping-bag',
          stars: 156,
          views: '3.2k',
          isHovered: false,
          year: '2022–2023',
          role: 'Full Stack Developer (Solo), UI/UX Designer'
        },
        {
          id: 3,
          title: 'Sentiment Analysis Web App Using Trained ML Models',
          description: 'Web application that performs sentiment analysis on text data using custom-trained machine learning models for accurate emotion detection.',
          category: 'AI/ML',
          technologies: ['Python', 'Scikit-learn', 'Flask', 'React'],
          color: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
          icon: 'pixelart-icons-font-chart',
          stars: 89,
          views: '1.8k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer (Solo), UI/UX Designer'
        },
        {
          id: 4,
          title: 'AI-Powered Image Recognition Web App using Teachable Machine',
          description: 'Interactive web application leveraging Google Teachable Machine for real-time image recognition and classification tasks.',
          category: 'AI/ML',
          technologies: ['JavaScript', 'TensorFlow.js', 'Vue.js', 'Teachable Machine'],
          color: 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)',
          icon: 'pixelart-icons-font-image',
          stars: 201,
          views: '4.1k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer'
        },
        {
          id: 5,
          title: 'Real-Time Illegal Dumpsite Detection and Mapping System',
          description: 'Advanced mapping system that uses AI and real-time data processing to detect and map illegal dumpsites for environmental monitoring.',
          category: 'Mapping Systems',
          technologies: ['Python', 'OpenCV', 'Mapbox', 'React', 'Socket.io'],
          color: 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)',
          icon: 'pixelart-icons-font-map',
          stars: 312,
          views: '5.7k',
          isHovered: false,
          year: '2024–2025',
          role: 'Full Stack Developer (Solo), UI/UX Designer'
        },
        {
          id: 6,
          title: 'AI-Powered DevSecOps Platform for Continuous Security Audits',
          description: 'Comprehensive DevSecOps platform that automates security audits and compliance checks using AI-driven analysis and monitoring.',
          category: 'DevSecOps',
          technologies: ['Docker', 'Kubernetes', 'Python', 'Jenkins', 'Vue.js'],
          color: 'linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%)',
          icon: 'pixelart-icons-font-shield',
          stars: 428,
          views: '6.3k',
          isHovered: false,
          year: '2025–ongoing',
          role: 'Full Stack Developer, UI/UX Designer, Project Manager'
        },        {
          id: 7,
          title: 'Custom Chatbot Creation Platform with AI Personas',
          description: 'Platform enabling users to create custom chatbots with distinct AI personas for various business and personal applications.',
          category: 'AI/ML',
          technologies: ['Python', 'OpenAI API', 'React', 'Node.js', 'WebSocket'],
          color: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
          icon: 'pixelart-icons-font-chat',
          stars: 195,
          views: '3.8k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer (Solo), UI/UX Designer'
        },
        {
          id: 8,
          title: 'Memecoin Website',
          description: 'This website explores the world of memecoins, covering their history, rise in popularity, investment risks, and impact on cryptocurrency, while providing insights on how to get started and navigate the speculative market.',
          category: 'Websites',
          technologies: ['Vue.js', 'Nuxt.js', 'CSS3', 'Chart.js', 'CoinGecko API'],
          color: 'linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%)',
          icon: 'pixelart-icons-font-coin',
          stars: 87,
          views: '1.9k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer, UI/UX Designer'
        },
        {
          id: 9,
          title: 'Botify Website',
          description: 'Modern and sleek website showcasing bot automation services and AI-powered solutions for businesses looking to streamline their operations.',
          category: 'Websites',
          technologies: ['React', 'Next.js', 'Tailwind CSS', 'Framer Motion'],
          color: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
          icon: 'pixelart-icons-font-robot',
          stars: 132,
          views: '2.4k',
          isHovered: false,
          year: '2023–2024',
          role: 'Full Stack Developer, UI/UX Designer'
        }
      ]
    }
  },
  computed: {
    filteredProjects() {
      if (this.activeFilter === 'All') {
        return this.projects
      }
      return this.projects.filter(project => project.category === this.activeFilter)    }
  },
  mounted() {
    this.initScrollAnimations()
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect()
    }
  },
  methods: {
    initScrollAnimations() {
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate')
            
            // Animate filter buttons
            if (entry.target === this.$refs.projectsFilter) {
              const filterBtns = entry.target.querySelectorAll('.filter-btn')
              filterBtns.forEach((btn, index) => {
                setTimeout(() => {
                  btn.classList.add('animate')
                }, index * 100)
              })
            }
            
            // Animate project cards with stagger
            if (entry.target === this.$refs.projectsGrid) {
              const projectCards = entry.target.querySelectorAll('.project-card')
              projectCards.forEach((card, index) => {
                setTimeout(() => {
                  card.classList.add('animate')
                }, index * 150)
              })
            }
            
            this.observer.unobserve(entry.target)
          }
        })
      }, {
        threshold: 0.1,
        rootMargin: '-30px'
      })

      const elementsToObserve = [
        this.$refs.sectionHeader,
        this.$refs.projectsFilter,
        this.$refs.projectsGrid
      ]

      elementsToObserve.forEach(el => {
        if (el) {
          this.observer.observe(el)
        }
      })
    },    filterProjects(category) {
      this.activeFilter = category
      
      // Re-trigger animations for the new filtered projects only
      this.$nextTick(() => {
        // Only target project cards within the projects grid, not filter buttons
        const projectsGrid = this.$refs.projectsGrid
        if (projectsGrid) {
          const projectCards = projectsGrid.querySelectorAll('.project-card')
          
          // Remove existing animations from project cards only
          projectCards.forEach(card => {
            card.classList.remove('animate')
          })
          
          // Add animations back with stagger
          setTimeout(() => {
            projectCards.forEach((card, index) => {
              setTimeout(() => {
                card.classList.add('animate')
              }, index * 100)
            })
          }, 150)
        }
        
        // Ensure filter buttons stay animated/visible
        const filterBtns = this.$refs.projectsFilter?.querySelectorAll('.filter-btn')
        if (filterBtns) {
          filterBtns.forEach(btn => {
            btn.classList.add('animate')
          })
        }
      })
    }
  }
}
</script>

<style scoped>
.projects {
  background: #000;
  border-bottom: 1px solid #fff;
}

/* 8-bit Projects Section */
.projects {
  background: 
    linear-gradient(135deg, #001 25%, #112 25%),
    linear-gradient(-135deg, #001 25%, #112 25%),
    linear-gradient(135deg, #112 75%, #001 75%),
    linear-gradient(-135deg, #112 75%, #001 75%);
  background-size: 30px 30px;
  background-position: 0 0, 0 15px, 15px -15px, -15px 0px;
  border-bottom: 1px solid #fff;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

/* 8-bit Title */
.pixel-title {
  font-size: 3rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 1rem;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 
    2px 2px 0 #333,
    4px 4px 0 #666;
}

.glitch-char {
  display: inline-block;
  position: relative;
  transition: all 0.1s ease;
}

.glitch-char:nth-child(2n) {
  animation: subtleGlitch 10s infinite;
  animation-delay: 2s;
}

.glitch-char:nth-child(7n) {
  animation: subtleGlitch 12s infinite;
  animation-delay: 6s;
}

@keyframes subtleGlitch {
  0%, 97%, 100% {
    transform: translateX(0);
    color: #fff;
    text-shadow: 2px 2px 0 #333, 4px 4px 0 #666;
  }
  98% {
    transform: translateX(2px);
    color: #ff0;
    text-shadow: -2px 2px 0 #0ff, 4px 4px 0 #f0f;
  }
}

.pixel-line {
  width: 120px;
  height: 4px;
  background: #fff;
  margin: 0 auto 1.5rem;
  position: relative;
}

.pixel-line::before,
.pixel-line::after {
  content: '';
  position: absolute;
  width: 8px;
  height: 8px;
  background: #fff;
  top: -2px;
}

.pixel-line::before {
  left: -12px;
}

.pixel-line::after {
  right: -12px;
}

.pixel-text {
  font-size: 1.2rem;
  color: #ccc;
  max-width: 700px;
  margin: 0 auto;
  font-family: 'Space Mono', monospace;
}

.glitch-word {
  display: inline-block;
  transition: all 0.2s ease;
}

.glitch-word:nth-child(3n):hover {
  animation: wordGlitch 0.4s ease-in-out;
}

@keyframes wordGlitch {
  0%, 80%, 100% {
    transform: translateX(0);
    color: inherit;
  }
  20% {
    transform: translateX(1px);
    color: #f0f;
  }
}



.section-line {
  width: 60px;
  height: 2px;
  background: #fff;
  margin: 0 auto 1.5rem;
}

.section-description {
  font-size: 1.1rem;
  color: #999;
  max-width: 600px;
  margin: 0 auto;
}

.projects-filter {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.75rem 1.5rem;
  border: 2px solid #333;
  background: #000;
  color: #999;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 700;
  font-family: 'Space Mono', monospace;
  text-transform: uppercase;
  font-size: 0.8rem;
  letter-spacing: 1px;
  opacity: 1 !important; /* Prevent animation interference */
  visibility: visible !important; /* Ensure always visible */
  pointer-events: auto !important; /* Ensure always clickable */
}

.filter-btn:hover {
  background: #000;
  color: #fff;
  border-color: #fff;
}

.filter-btn.active {
  background: #fff;
  color: #000;
  border-color: #fff;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.project-card {
  background: #000;
  border: 2px solid #fff;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.project-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  background: #000 !important;
}

.project-icon {
  font-size: 3rem;
  color: white;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-overlay.visible {
  opacity: 1;
}

.project-links {
  display: flex;
  gap: 1rem;
}

.project-link {
  width: 50px;
  height: 50px;
  background: #000;
  border: 1px solid #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  text-decoration: none;
  transition: transform 0.3s ease;
  font-size: 1.2rem;
}

.project-link:hover {
  transform: scale(1.1);
}

.project-content {  padding: 2rem;
}

.project-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.project-category {
  font-size: 0.8rem;
  color: #999;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-family: 'Space Mono', monospace;
}

.project-year {
  font-size: 0.75rem;
  color: #0f0;
  font-weight: 600;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  background: rgba(0, 255, 0, 0.1);
  padding: 0.2rem 0.5rem;
  border: 1px solid #0f0;
  border-radius: 2px;
}

.project-title {
  font-size: 1.3rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 1rem;
  font-family: 'Space Mono', monospace;
}

.project-description {
  color: #ccc;
  line-height: 1.6;
  margin-bottom: 1rem;
  font-size: 0.9rem;
}

.project-role {
  margin-bottom: 1.5rem;
  padding: 0.75rem;
  background: rgba(255, 255, 255, 0.05);
  border-left: 3px solid #fff;
  border-radius: 2px;
}

.role-label {
  font-size: 0.75rem;
  color: #fff;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  margin-right: 0.5rem;
}

.role-text {
  font-size: 0.8rem;
  color: #ccc;
  font-family: 'Space Mono', monospace;
  line-height: 1.4;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  padding: 0.25rem 0.75rem;
  background: #000;
  color: #fff;
  font-size: 0.7rem;
  font-weight: 700;
  font-family: 'Space Mono', monospace;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.project-stats {
  display: flex;
  gap: 1.5rem;
  color: #999;
  font-size: 0.8rem;
  font-family: 'Space Mono', monospace;
}

.stat {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.stat-icon {
  font-size: 1rem;
}

.projects-cta {
  text-align: center;
  padding: 3rem 0;
}

.projects-cta p {
  font-size: 1.2rem;
  color: #999;
  margin-bottom: 1.5rem;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .projects-filter {
    gap: 0.5rem;
  }
  
  .filter-btn {
    padding: 0.5rem 1rem;
    font-size: 0.9rem;
  }
    .project-content {
    padding: 1.5rem;
  }
}

/* 8-bit Scroll Animations */
.pixel-matrix-in {
  opacity: 1; /* Changed from 0 to 1 to make title always visible */
  transform: scale(1) rotateX(0deg); /* Changed to default visible state */
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-matrix-in.animate {
  opacity: 1;
  transform: scale(1) rotateX(0deg);
  animation: pixelMatrixFlicker 0.5s ease-in-out 0.6s;
}

.pixel-expand {
  width: 0;
  transition: width 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-expand.animate {
  width: 120px;
  animation: pixelLineCharge 0.6s ease-in-out 0.4s;
}

.pixel-fade-up {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.7s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-fade-up.animate {
  opacity: 0.9;
  transform: translateY(0);
}

.pixel-filter-slide {
  opacity: 0;
  transform: translateY(-30px);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-filter-slide.animate {
  opacity: 1;
  transform: translateY(0);
}

.pixel-filter-btn {
  opacity: 1; /* Always visible instead of 0 */
  transform: translateY(0) scale(1); /* Start in final position */
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-filter-btn:not(.animate) {
  opacity: 0; /* Only fade out if not animated yet */
  transform: translateY(-20px) scale(0.8);
}

.pixel-filter-btn.animate {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.pixel-grid-container {
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-grid-container.animate {
  opacity: 1;
  transform: translateY(0);
}

.pixel-project-card {
  opacity: 0;
  transform: translateY(60px) scale(0.8) rotateX(30deg);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-project-card.animate {
  opacity: 1;
  transform: translateY(0) scale(1) rotateX(0deg);
}

/* Ensure smooth transitions during filtering */
.projects-grid {
  transition: opacity 0.3s ease;
}

.project-card {
  transition: all 0.4s ease;
}

/* Vue transition classes for smooth filtering */
.project-filter-enter-active,
.project-filter-leave-active {
  transition: all 0.4s ease;
}

.project-filter-enter-from {
  opacity: 0;
  transform: translateY(30px) scale(0.8);
}

.project-filter-leave-to {
  opacity: 0;
  transform: translateY(-30px) scale(0.8);
}

@keyframes pixelMatrixFlicker {
  0%, 100% { 
    filter: hue-rotate(0deg) brightness(1);
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
  }
  25% { 
    filter: hue-rotate(90deg) brightness(1.2);
    text-shadow: 0 0 15px rgba(0, 255, 0, 0.8);
  }
  50% { 
    filter: hue-rotate(180deg) brightness(0.8);
    text-shadow: 0 0 20px rgba(255, 0, 255, 0.8);
  }
  75% { 
    filter: hue-rotate(270deg) brightness(1.1);
    text-shadow: 0 0 15px rgba(0, 255, 255, 0.8);
  }
}

@keyframes pixelLineCharge {
  0% { 
    box-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
    background: #fff;
  }
  33% { 
    box-shadow: 0 0 20px rgba(255, 255, 0, 0.8), 0 0 40px rgba(255, 255, 0, 0.4);
    background: linear-gradient(90deg, #fff, #ff0, #fff);
  }
  66% { 
    box-shadow: 0 0 25px rgba(0, 255, 255, 0.8), 0 0 50px rgba(0, 255, 255, 0.4);
    background: linear-gradient(90deg, #fff, #0ff, #fff);
  }
  100% { 
    box-shadow: 0 0 15px rgba(255, 255, 255, 0.6);
    background: #fff;
  }
}

/* Enhanced hover effects for animated elements */
.pixel-project-card.animate:hover {
  animation: pixelProjectGlow 0.8s ease-in-out;
}

.pixel-filter-btn.animate:hover {
  animation: pixelButtonPulse 0.4s ease-in-out;
}

@keyframes pixelProjectGlow {
  0%, 100% { 
    transform: scale(1);
    box-shadow: 0 5px 20px rgba(255, 255, 255, 0.1);
  }
  50% { 
    transform: scale(1.02);
    box-shadow: 
      0 10px 30px rgba(255, 255, 255, 0.2),
      0 0 20px rgba(0, 255, 255, 0.3),
      inset 0 0 20px rgba(255, 255, 255, 0.1);
  }
}

@keyframes pixelButtonPulse {
  0%, 100% { transform: scale(1); }
  50% { 
    transform: scale(1.1);
    box-shadow: 0 0 15px rgba(255, 255, 255, 0.4);
  }
}
</style>
