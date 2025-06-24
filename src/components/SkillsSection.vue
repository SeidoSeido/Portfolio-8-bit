<template>
  <section id="skills" class="skills section">
    <div class="container">      <div class="section-header" ref="sectionHeader">
        <h2 class="section-title pixel-title pixel-type-in">
          <span class="glitch-char">S</span><span class="glitch-char">K</span><span class="glitch-char">I</span><span class="glitch-char">L</span><span class="glitch-char">L</span><span class="glitch-char">S</span>
          <span class="space">&nbsp;</span><span class="glitch-char">&</span><span class="space">&nbsp;</span>
          <span class="glitch-char">E</span><span class="glitch-char">X</span><span class="glitch-char">P</span><span class="glitch-char">E</span><span class="glitch-char">R</span><span class="glitch-char">T</span><span class="glitch-char">I</span><span class="glitch-char">S</span><span class="glitch-char">E</span>
        </h2>
        <div class="section-line pixel-line pixel-expand"></div>
        <p class="section-description pixel-text pixel-fade-in">
          <span class="glitch-word">Technologies</span> <span class="glitch-word">and</span> <span class="glitch-word">tools</span> <span class="glitch-word">I</span> <span class="glitch-word">use</span> <span class="glitch-word">to</span> <span class="glitch-word">bring</span> <span class="glitch-word">ideas</span> <span class="glitch-word">to</span> <span class="glitch-word">life</span>
        </p>
      </div>
      
      <div class="skills-content">
        <div class="skills-category pixel-slide-right" ref="frontendCategory">
          <h3 class="category-title">Frontend Development</h3>
          <div class="skills-grid">            <div class="skill-item pixel-skill-item" v-for="skill in frontendSkills" :key="skill.name">
              <div class="skill-icon">
                <i :class="skill.icon"></i>
              </div>
              <div class="skill-info">
                <h4 class="skill-name">{{ skill.name }}</h4>
                <div class="skill-bar">
                  <div class="skill-progress pixel-progress-bar" :style="{ width: skill.level + '%' }"></div>
                </div>
                <span class="skill-percentage">{{ skill.level }}%</span>
              </div>
            </div>
          </div>
        </div>
        
        <div class="skills-category pixel-slide-left" ref="toolsCategory">
          <h3 class="category-title">Tools & Others</h3>
          <div class="skills-grid">            <div class="skill-item pixel-skill-item" v-for="skill in toolsSkills" :key="skill.name">
              <div class="skill-icon">
                <i :class="skill.icon"></i>
              </div>
              <div class="skill-info">
                <h4 class="skill-name">{{ skill.name }}</h4>
                <div class="skill-bar">
                  <div class="skill-progress pixel-progress-bar" :style="{ width: skill.level + '%' }"></div>
                </div>
                <span class="skill-percentage">{{ skill.level }}%</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="certifications">
        <h3 class="category-title">Certifications & Achievements</h3>
        <div class="cert-grid">          <div class="cert-item" v-for="cert in certifications" :key="cert.name">
            <div class="cert-icon">
              <i class="pixelart-icons-font-trophy"></i>
            </div>
            <div class="cert-info">
              <h4>{{ cert.name }}</h4>
              <p>{{ cert.issuer }}</p>
              <span class="cert-year">{{ cert.year }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SkillsSection',
  data() {
    return {
      observer: null,      frontendSkills: [        { name: 'Vue.js', icon: 'pixelart-icons-font-heart', level: 95 },
        { name: 'React', icon: 'pixelart-icons-font-sun', level: 90 },
        { name: 'JavaScript', icon: 'pixelart-icons-font-code', level: 95 },
        { name: 'TypeScript', icon: 'pixelart-icons-font-script', level: 85 },
        { name: 'HTML5', icon: 'pixelart-icons-font-article', level: 98 },
        { name: 'CSS3', icon: 'pixelart-icons-font-image', level: 95 },
        { name: 'Sass/SCSS', icon: 'pixelart-icons-font-colors-swatch', level: 90 },
        { name: 'Tailwind CSS', icon: 'pixelart-icons-font-paint-bucket', level: 88 }
      ],
      toolsSkills: [        { name: 'Git', icon: 'pixelart-icons-font-git-branch', level: 92 },
        { name: 'Webpack', icon: 'pixelart-icons-font-archive', level: 80 },
        { name: 'Vite', icon: 'pixelart-icons-font-zap', level: 85 },
        { name: 'Node.js', icon: 'pixelart-icons-font-server', level: 75 },
        { name: 'Docker', icon: 'pixelart-icons-font-building', level: 70 },
        { name: 'AWS', icon: 'pixelart-icons-font-cloud', level: 65 },
        { name: 'Figma', icon: 'pixelart-icons-font-edit', level: 85 },
        { name: 'Adobe XD', icon: 'pixelart-icons-font-device-tablet', level: 80 }
      ],
      certifications: [
        {
          name: 'Vue.js Certified Developer',
          issuer: 'Vue School',
          year: '2023'
        },
        {
          name: 'Cisco Networking Basics',
          issuer: 'Cisco',
          year: '2022'
        },
        {
          name: 'Google Analytics Certified',
          issuer: 'Google',
          year: '2022'
        },
        {
          name: 'Frontend Masters Certificate',
          issuer: 'Frontend Masters',
          year: '2021'
        }
      ]
    }
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
            
            // Animate skill items with stagger
            if (entry.target === this.$refs.frontendCategory || entry.target === this.$refs.toolsCategory) {
              const skillItems = entry.target.querySelectorAll('.skill-item')
              const progressBars = entry.target.querySelectorAll('.skill-progress')
              
              skillItems.forEach((item, index) => {
                setTimeout(() => {
                  item.classList.add('animate')
                }, index * 100)
              })
              
              progressBars.forEach((bar, index) => {
                setTimeout(() => {
                  bar.classList.add('animate')
                }, index * 150 + 300)
              })
            }
            
            this.observer.unobserve(entry.target)
          }
        })
      }, {
        threshold: 0.1,
        rootMargin: '-50px'
      })

      const elementsToObserve = [
        this.$refs.sectionHeader,
        this.$refs.frontendCategory,
        this.$refs.toolsCategory
      ]

      elementsToObserve.forEach(el => {
        if (el) {
          this.observer.observe(el)
        }
      })
    }
  }
}
</script>

<style scoped>
/* Skills Section */
.skills {
  background: #000;
  border-bottom: 1px solid #fff;
  position: relative;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
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

.glitch-char:nth-child(4n) {
  animation: subtleGlitch 7s infinite;
  animation-delay: 1s;
}

.glitch-char:nth-child(6n) {
  animation: subtleGlitch 9s infinite;
  animation-delay: 4s;
}

@keyframes subtleGlitch {
  0%, 97%, 100% {
    transform: translateX(0);
    color: #fff;
    text-shadow: 2px 2px 0 #333, 4px 4px 0 #666;
  }
  98% {
    transform: translateX(1px);
    color: #f0f;
    text-shadow: -2px 2px 0 #0ff, 4px 4px 0 #ff0;
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

.glitch-word:nth-child(2n):hover {
  animation: wordGlitch 0.4s ease-in-out;
}

@keyframes wordGlitch {
  0%, 80%, 100% {
    transform: translateX(0);
    color: inherit;
  }
  20% {
    transform: translateX(1px);
    color: #0ff;
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

.skills-content {
  display: grid;
  gap: 4rem;
  margin-bottom: 4rem;
}

.skills-category {
  background: #000;
  padding: 2.5rem;
  border: 1px solid #fff;
  box-shadow: none;
}

.category-title {
  font-size: 1.3rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 2rem;
  text-align: center;
  font-family: 'Space Mono', monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

/* Skill Items */
.skill-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  background: #000;
  border: 2px solid #fff;
  transition: all 0.2s ease;
  position: relative;
}

.skill-item:hover {
  transform: translateY(-2px);
  background: #111;
  box-shadow: 
    0 4px 0 #666,
    0 0 20px rgba(255, 255, 255, 0.2);
}

/* Skill Icon */
.skill-icon {
  font-size: 1.5rem;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000;
  border: 2px solid #fff;
  color: #fff;
}

.skill-info {
  flex: 1;
}

.skill-name {
  font-size: 1rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 0.5rem;
  font-family: 'Space Mono', monospace;
}

.skill-bar {
  width: 100%;
  height: 4px;
  background: #333;
  overflow: hidden;
  margin-bottom: 0.25rem;
}

.skill-progress {
  height: 100%;
  background: #fff;
  transition: width 1s ease;
}

.skill-percentage {
  font-size: 0.8rem;
  color: #fff;
  font-weight: 700;
  font-family: 'Space Mono', monospace;
}

.certifications {
  background: #000;
  padding: 2.5rem;
  border: 1px solid #fff;
  box-shadow: none;
}

.cert-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.cert-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: #111;
  border: 1px solid #333;
  transition: transform 0.3s ease;
}

.cert-item:hover {
  transform: translateY(-3px);
  border-color: #fff;
}

.cert-icon {
  font-size: 1.5rem;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #fff;
  color: #000;
}

.cert-info h4 {
  font-size: 1rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 0.25rem;
  font-family: 'Space Mono', monospace;
}

.cert-info p {
  color: #ccc;
  font-size: 0.9rem;
  margin-bottom: 0.25rem;
}

.cert-year {
  font-size: 0.8rem;
  color: #fff;
  font-weight: 700;
  font-family: 'Space Mono', monospace;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
    letter-spacing: 2px;
    line-height: 1.3;
  }
  
  .skills-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .cert-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .skills-category,
  .certifications {
    padding: 1.5rem;
  }
  
  .category-title {
    font-size: 1.2rem;
    margin-bottom: 1rem;
    line-height: 1.3;
  }
  
  .skill-item {
    margin-bottom: 1rem;
  }
  
  .skill-name {
    font-size: 0.7rem;
    margin-bottom: 0.5rem;
  }
  
  .skill-level {
    font-size: 0.6rem;
  }
  
  .skill-bar {
    height: 6px;
  }
  
  .cert-item {
    padding: 1rem;
  }
  
  .cert-title {
    font-size: 0.8rem;
    margin-bottom: 0.3rem;
  }
  
  .cert-org {
    font-size: 0.7rem;
  }
}

@media (max-width: 480px) {
  .section-title {
    font-size: 1.4rem;
    letter-spacing: 0.5px;
    line-height: 1.2;
    word-break: break-word;
  }
  
  .skills-grid,
  .cert-grid {
    gap: 1rem;
  }
  
  .skills-category,
  .certifications {
    padding: 1.2rem;
  }
  
  .category-title {
    font-size: 1rem;
  }
  
  .skill-name {
    font-size: 0.65rem;
  }
  
  .skill-level {
    font-size: 0.55rem;
  }
  
  .skill-bar {
    height: 5px;
  }
  
  .cert-item {
    padding: 0.8rem;
  }
  
  .cert-title {
    font-size: 0.7rem;
  }
    .cert-org {
    font-size: 0.65rem;
  }
}

@media (max-width: 400px) {
  .section-title {
    font-size: 1.2rem;
    letter-spacing: 0px;
    line-height: 1.1;
    word-break: break-word;
  }
}

/* 8-bit Scroll Animations */
.pixel-type-in {
  opacity: 1; /* Changed from 0 to 1 to make title always visible */
  animation: pixelTypeWriter 2s steps(20) forwards;
}

.pixel-type-in.animate {
  opacity: 1;
  animation: pixelTypeWriter 1s steps(20) forwards, pixelGlitch 0.3s ease-in-out 1.2s;
}

.pixel-expand {
  width: 0;
  transition: width 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-expand.animate {
  width: 120px;
  animation: pixelSparkle 0.5s ease-in-out 0.8s;
}

.pixel-fade-in {
  opacity: 0;
  transform: translateY(15px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-fade-in.animate {
  opacity: 0.9;
  transform: translateY(0);
}

.pixel-slide-right {
  opacity: 0;
  transform: translateX(-100px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-slide-right.animate {
  opacity: 1;
  transform: translateX(0);
}

.pixel-slide-left {
  opacity: 0;
  transform: translateX(100px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-slide-left.animate {
  opacity: 1;
  transform: translateX(0);
}

.pixel-skill-item {
  opacity: 0;
  transform: translateY(30px) scale(0.8);
  transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-skill-item.animate {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.pixel-progress-bar {
  width: 0 !important;
  transition: width 1.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  position: relative;
}

.pixel-progress-bar.animate {
  width: var(--target-width) !important;
  animation: pixelProgressGlow 0.3s ease-in-out 1.2s;
}

@keyframes pixelTypeWriter {
  0% { width: 0; }
  100% { width: 100%; }
}

@keyframes pixelGlitch {
  0%, 100% { transform: translateX(0); filter: hue-rotate(0deg); }
  25% { transform: translateX(-2px); filter: hue-rotate(90deg); }
  50% { transform: translateX(2px); filter: hue-rotate(180deg); }
  75% { transform: translateX(-1px); filter: hue-rotate(270deg); }
}

@keyframes pixelSparkle {
  0%, 100% { box-shadow: 0 0 5px rgba(255, 255, 255, 0.5); }
  25% { box-shadow: 0 0 15px rgba(255, 255, 0, 0.8), 0 0 25px rgba(255, 255, 0, 0.4); }
  50% { box-shadow: 0 0 20px rgba(0, 255, 255, 0.8), 0 0 30px rgba(0, 255, 255, 0.4); }
  75% { box-shadow: 0 0 15px rgba(255, 0, 255, 0.8), 0 0 25px rgba(255, 0, 255, 0.4); }
}

@keyframes pixelProgressGlow {
  0%, 100% { box-shadow: inset 0 0 10px rgba(255, 255, 255, 0.3); }
  50% { box-shadow: inset 0 0 20px rgba(0, 255, 0, 0.6), 0 0 10px rgba(0, 255, 0, 0.4); }
}

/* Enhanced hover effects */
.pixel-skill-item.animate:hover {
  animation: pixelSkillPulse 0.6s ease-in-out;
}

.pixel-skill-item.animate:hover .skill-icon {
  animation: pixelIconSpin 0.8s ease-in-out;
}

@keyframes pixelSkillPulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); box-shadow: 0 0 20px rgba(255, 255, 255, 0.2); }
}

@keyframes pixelIconSpin {
  0% { transform: rotate(0deg) scale(1); }
  50% { transform: rotate(180deg) scale(1.1); }
  100% { transform: rotate(360deg) scale(1); }
}
</style>
