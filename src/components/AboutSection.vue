<template>
  <section id="about" class="about section">
    <div class="container">      <div class="section-header" ref="sectionHeader">
        <h2 class="section-title pixel-title pixel-glitch-in">
          <span class="glitch-char">A</span><span class="glitch-char">B</span><span class="glitch-char">O</span><span class="glitch-char">U</span><span class="glitch-char">T</span>
          <span class="space">&nbsp;</span>
          <span class="glitch-char">M</span><span class="glitch-char">E</span>
        </h2>
        <div class="section-line pixel-line pixel-expand"></div>
      </div>
      
      <div class="about-content">
        <div class="about-text">          <div class="text-block pixel-slide-up" ref="textBlock1">
            <h3>Passionate Frontend Developer</h3>
            <p>
              Aspiring Computer Science professional with a strong foundation in web and software development. Passionate
              about leveraging technology to enhance user experiences, with experience in AI-driven curriculum evaluation
              and e-commerce platforms. Skilled in problem-solving, interface design, and team collaboration, eager to
              contribute technical expertise to innovative projects in a dynamic environment.
            </p>
          </div>
          
          <div class="text-block pixel-slide-up" ref="textBlock2">
            <h3>My Approach</h3>
            <p>
              I believe in writing clean, maintainable code and creating user interfaces that are 
              not only visually appealing but also accessible and performant. I enjoy collaborating 
              with designers and backend developers to bring ideas to life.
            </p>
          </div>
          
          <div class="stats-grid pixel-counter-animation" ref="statsGrid">            <div class="stat-item pixel-stat-bounce">
              <div class="stat-number">5+</div>
              <div class="stat-label">Projects Completed</div>
            </div>
            <div class="stat-item pixel-stat-bounce">
              <div class="stat-number">2+</div>
              <div class="stat-label">Years Experience</div>
            </div>
            <div class="stat-item pixel-stat-bounce">
              <div class="stat-number">2+</div>
              <div class="stat-label">Happy Clients</div>
            </div>
            <div class="stat-item pixel-stat-bounce">
              <div class="stat-number">∞</div>
              <div class="stat-label">Cups of Coffee</div>
            </div>
          </div>
        </div>        <div class="about-image">
          <div class="retro-display" ref="retroDisplay">
            <!-- Simple Retro Screen -->
            <div class="retro-screen">
              <div class="screen-header">
                <div class="screen-title">DEVELOPER.EXE</div>
                <div class="screen-status">●●●</div>
              </div>
              
              <!-- Simple Retro Content -->
              <div class="screen-content">
                <div class="profile-section">
                  <div class="profile-line">
                    <span class="label">NAME:</span>
                    <span class="value">SIR LAUDATO</span>
                  </div>
                  <div class="profile-line">
                    <span class="label">ROLE:</span>
                    <span class="value">FRONTEND DEV</span>
                  </div>
                  <div class="profile-line">
                    <span class="label">STATUS:</span>
                    <span class="value blinking">CODING...</span>
                  </div>
                </div>
                
                <!-- Simple Tech Stack Display -->
                <div class="tech-section">
                  <div class="section-label">TECH STACK:</div>
                  <div class="tech-grid">                    <div class="tech-item" v-for="tech in techStack" :key="tech.name">
                      <div class="tech-icon">
                        <i :class="tech.icon"></i>
                        <span class="icon-fallback" v-if="!tech.icon">{{ tech.fallback }}</span>
                      </div>
                      <span>{{ tech.name }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',  data() {
    return {
      observer: null,      techStack: [
        { name: 'VUE', icon: 'pixelart-icons-font-zap', fallback: '⚡' },
        { name: 'REACT', icon: 'pixelart-icons-font-settings', fallback: '⚛️' },
        { name: 'JS', icon: 'pixelart-icons-font-code', fallback: '💻' },
        { name: 'CSS', icon: 'pixelart-icons-font-paint-bucket', fallback: '🎨' },
        { name: 'NODE', icon: 'pixelart-icons-font-server', fallback: '🖥️' },
        { name: 'GIT', icon: 'pixelart-icons-font-git-branch', fallback: '📦' }
      ]
    }
  },  mounted() {
    this.initScrollAnimations()
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect()
    }
  },  methods: {
    initScrollAnimations() {
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate')
            
            // Special handling for stats
            if (entry.target === this.$refs.statsGrid) {
              const stats = entry.target.querySelectorAll('.stat-item')
              stats.forEach((stat, index) => {
                setTimeout(() => {
                  stat.classList.add('animate')
                }, index * 150)
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
        this.$refs.textBlock1,
        this.$refs.textBlock2,
        this.$refs.statsGrid,
        this.$refs.retroDisplay
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
/* About Section with Moving Lines Background */
.about {
  background: #000;
  color: #fff;
  border-bottom: 1px solid #fff;
  position: relative;
  overflow: hidden;
}

/* Enhanced Moving Horizontal Scanlines Only */
.about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 3px,
    rgba(255, 255, 255, 0.08) 3px,
    rgba(255, 255, 255, 0.08) 6px
  );
  animation: movingLines 3s linear infinite;
  pointer-events: none;
  z-index: 0;
}

/* Secondary Layer - Only Horizontal Lines */
.about::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 8px,
    rgba(255, 255, 255, 0.04) 8px,
    rgba(255, 255, 255, 0.04) 12px
  );
  animation: movingLinesSecondary 4s linear infinite reverse;
  pointer-events: none;
  z-index: 0;
}

@keyframes movingLines {
  0% { transform: translateY(0); }
  100% { transform: translateY(6px); }
}

@keyframes movingLinesSecondary {
  0% { transform: translateY(0); }
  100% { transform: translateY(12px); }
}



.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

/* 8-bit Title with Glitch Effect */
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

.glitch-char:nth-child(3n) {
  animation: subtleGlitch 6s infinite;
  animation-delay: 0s;
}

.glitch-char:nth-child(5n) {
  animation: subtleGlitch 8s infinite;
  animation-delay: 3s;
}

@keyframes subtleGlitch {
  0%, 98%, 100% {
    transform: translateX(0);
    color: #fff;
    text-shadow: 2px 2px 0 #333, 4px 4px 0 #666;
  }
  99% {
    transform: translateX(2px);
    color: #0f0;
    text-shadow: -2px 2px 0 #f00, 4px 4px 0 #00f;
  }
}



.pixel-line {
  width: 100px;
  height: 4px;
  background: #fff;
  margin: 0 auto;
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
  left: -10px;
}

.pixel-line::after {
  right: -10px;
}

.section-line {
  width: 60px;
  height: 2px;
  background: #fff;
  margin: 0 auto;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.text-block {
  margin-bottom: 2rem;
}

.text-block h3 {
  font-size: 1.2rem;
  color: #fff;
  margin-bottom: 1rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.text-block p {
  font-size: 1rem;
  line-height: 1.6;
  color: #ccc;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
  margin-top: 3rem;
}

/* 8-bit Stats */
.stat-item {
  text-align: center;
  padding: 1.5rem;
  background: #000;
  border: 2px solid #fff;
  transition: all 0.2s ease;
  position: relative;
  overflow: hidden;
}

.stat-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    45deg,
    transparent,
    transparent 4px,
    rgba(255, 255, 255, 0.05) 4px,
    rgba(255, 255, 255, 0.05) 8px
  );
}

.stat-item:hover {
  background: #111;
  transform: translateY(-2px);
  box-shadow: 
    0 4px 0 #666,
    0 0 20px rgba(255, 255, 255, 0.2);
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 0.5rem;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  text-shadow: 2px 2px 0 #333;
  position: relative;
  z-index: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: #ccc;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  z-index: 1;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.about-image {
  position: relative;
}

/* Simple Retro Display */
.retro-display {
  max-width: 450px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease;
}

.retro-display.animate {
  opacity: 1;
  transform: translateY(0);
}

.retro-screen {
  background: #000;
  border: 3px solid #fff;
  padding: 0;
  font-family: 'Space Mono', monospace;
  box-shadow: 
    0 0 20px rgba(255, 255, 255, 0.2),
    inset 0 0 20px rgba(0, 255, 0, 0.1);
  position: relative;
}

/* Simple scanline effect */
.retro-screen::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(255, 255, 255, 0.03) 2px,
    rgba(255, 255, 255, 0.03) 4px
  );
  pointer-events: none;
  z-index: 1;
}

.screen-header {
  background: #333;
  padding: 12px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #fff;
}

.screen-title {
  color: #fff;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 1px;
}

.screen-status {
  color: #0f0;
  font-size: 0.8rem;
  letter-spacing: 2px;
}

.screen-content {
  padding: 25px 20px;
  position: relative;
  z-index: 2;
}

.profile-section {
  margin-bottom: 30px;
}

.profile-line {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
  padding: 8px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.label {
  color: #ccc;
  font-size: 0.85rem;
  font-weight: 400;
}

.value {
  color: #fff;
  font-size: 0.85rem;
  font-weight: 700;
}

.blinking {
  animation: blink 2s infinite;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0.3; }
}

.tech-section {
  margin-top: 25px;
}

.section-label {
  color: #0f0;
  font-size: 0.9rem;
  font-weight: 700;
  margin-bottom: 15px;
  letter-spacing: 1px;
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
}

.tech-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 12px 8px;
  border: 1px solid #666;
  background: rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  text-align: center;
}

.tech-item:hover {
  border-color: #0f0;
  background: rgba(0, 255, 0, 0.1);
  transform: translateY(-2px);
}

.tech-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 24px;
  margin-bottom: 8px;
}

.tech-item i {
  font-size: 1.5rem;
  color: #fff;
  transition: color 0.3s ease;
}

.tech-item:hover i {
  color: #0f0;
}

.icon-fallback {
  font-size: 1.5rem;
  display: block;
}

.tech-item span {  color: #ccc;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.5px;
}

/* 8-bit Scroll Animations */
.pixel-glitch-in {
  opacity: 1;
  transform: translateY(0);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-glitch-in.animate {
  opacity: 1;
  transform: translateY(0);
  animation: pixelGlitchEffect 0.3s ease-in-out 0.3s;
}

.pixel-expand {
  width: 0;
  transition: width 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-expand.animate {
  width: 80px;
  animation: pixelLineFlicker 0.4s ease-in-out 0.6s;
}

.pixel-slide-up {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-slide-up.animate {
  opacity: 1;
  transform: translateY(0);
}

.pixel-slide-up:nth-child(1).animate {
  transition-delay: 0.2s;
}

.pixel-slide-up:nth-child(2).animate {
  transition-delay: 0.4s;
}

.pixel-counter-animation {
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.7s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-counter-animation.animate {
  opacity: 1;
  transform: scale(1);
}

.pixel-stat-bounce {
  opacity: 0;
  transform: translateY(50px) scale(0.5);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-stat-bounce.animate {
  opacity: 1;
  transform: translateY(0) scale(1);
  animation: pixelStatPop 0.4s ease-in-out;
}

@keyframes pixelGlitchEffect {
  0% { transform: translateX(0); filter: hue-rotate(0deg); }
  25% { transform: translateX(-3px); filter: hue-rotate(90deg); }
  50% { transform: translateX(3px); filter: hue-rotate(180deg); }
  75% { transform: translateX(-2px); filter: hue-rotate(270deg); }
  100% { transform: translateX(0); filter: hue-rotate(0deg); }
}

@keyframes pixelLineFlicker {
  0%, 100% { box-shadow: 0 0 5px rgba(255, 255, 255, 0.5); }
  33% { box-shadow: 0 0 15px rgba(0, 255, 0, 0.7); }
  66% { box-shadow: 0 0 20px rgba(255, 0, 255, 0.7); }
}

@keyframes pixelStatPop {
  0% { transform: scale(1); }
  50% { transform: scale(1.1); box-shadow: 0 0 20px rgba(255, 255, 255, 0.3); }
  100% { transform: scale(1); }
}

@media (max-width: 768px) {
  .pixel-title {
    font-size: 2rem;
    letter-spacing: 2px;
    line-height: 1.3;
    margin-bottom: 1rem;
  }
  
  .about-content {
    grid-template-columns: 1fr;
    gap: 2rem;
    padding: 0 1rem;
  }
  
  .text-block {
    margin-bottom: 1.5rem;
  }
  
  .text-block h3 {
    font-size: 1rem;
    line-height: 1.4;
    margin-bottom: 0.8rem;
  }
  
  .text-block p {
    font-size: 0.9rem;
    line-height: 1.6;
  }
  
  .stats-grid {
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-top: 2rem;
  }
  
  .stat-item {
    padding: 1rem;
  }
  
  .stat-number {
    font-size: 1.5rem;
    margin-bottom: 0.3rem;
  }
  
  .stat-label {
    font-size: 0.7rem;
    line-height: 1.3;
  }
  
  .retro-screen {
    border-width: 2px;
  }
  
  .screen-header {
    padding: 10px 15px;
  }
  
  .screen-title {
    font-size: 0.8rem;
  }
  
  .screen-content {
    padding: 20px 15px;
  }
  
  .tech-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }
    .tech-item {
    padding: 10px 6px;
  }
  
  .tech-icon {
    height: 20px;
    margin-bottom: 6px;
  }
  
  .tech-item i,
  .icon-fallback {
    font-size: 1.2rem;
  }
  
  .tech-item span:last-child {
    font-size: 0.65rem;
  }
}

@media (max-width: 480px) {
  .pixel-title {
    font-size: 1.6rem;
    letter-spacing: 1px;
  }
  
  .about-content {
    padding: 0 0.5rem;
    gap: 1.5rem;
  }
  
  .text-block h3 {
    font-size: 0.9rem;
  }
  
  .text-block p {
    font-size: 0.85rem;
  }
  
  .stats-grid {
    grid-template-columns: 1fr;
    gap: 0.8rem;
    margin-top: 1.5rem;
  }
  
  .stat-item {
    padding: 0.8rem;
  }
  
  .stat-number {
    font-size: 1.3rem;
  }
  
  .stat-label {
    font-size: 0.65rem;
  }
  
  .retro-screen {
    border-width: 1px;
  }
  
  .screen-header {
    padding: 8px 12px;
  }
  
  .screen-title {
    font-size: 0.7rem;
  }
  
  .screen-content {
    padding: 15px 12px;
  }
  
  .profile-line {
    margin-bottom: 10px;
    padding: 6px 0;
  }
  
  .label, .value {
    font-size: 0.75rem;
  }
  
  .tech-grid {
    grid-template-columns: 1fr 1fr;
    gap: 8px;
  }
    .tech-item {
    padding: 8px 4px;
  }
  
  .tech-icon {
    height: 18px;
    margin-bottom: 6px;
  }
  
  .tech-item i,
  .icon-fallback {
    font-size: 1rem;
  }
  
  .tech-item span:last-child {
    font-size: 0.6rem;
  }
}

/* Content positioning */
.about .container {
  position: relative;
  z-index: 1;
}
</style>
