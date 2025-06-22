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
        <div class="about-text">
          <div class="text-block pixel-slide-up" ref="textBlock1">
            <h3>Passionate Frontend Developer</h3>
            <p>
              With over 5 years of experience in frontend development, I specialize in creating 
              exceptional digital experiences that combine beautiful design with robust functionality. 
              I'm passionate about staying up-to-date with the latest technologies and best practices 
              in web development.
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
        </div>
        
        <div class="about-image">
          <div class="image-placeholder">
            <div class="code-animation">
              <div class="code-line" v-for="(line, index) in codeLines" :key="index" :style="{ animationDelay: index * 0.2 + 's' }">
                {{ line }}
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
  name: 'AboutSection',
  data() {
    return {
      observer: null,      codeLines: [
        "const dev = {",
        "  name: 'Sir Laudato',",
        "  role: 'Frontend Dev',",
        "  skills: ['Vue', 'React'],",
        "  passion: 'Amazing UX',",
        "  coffee: '☕'.repeat(∞)",
        "};"
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
        this.$refs.statsGrid
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
/* 8-bit About Section */
.about {
  background: #000;
  color: #fff;
  border-bottom: 1px solid #fff;
  position: relative;
  overflow: hidden;
}

/* Enhanced 8-bit Screen Effect - More Visible Scanlines */
.about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent 0px,
    transparent 2px,
    rgba(0, 255, 0, 0.15) 2px,
    rgba(0, 255, 0, 0.15) 4px
  );
  animation: screenFlicker 4s linear infinite;
  opacity: 1;
}

/* Enhanced 8-bit Screen Effect - More Visible Pixel Grid */
.about::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  background: 
    radial-gradient(circle at 50% 50%, rgba(0, 255, 0, 0.3) 1px, transparent 1px),
    linear-gradient(90deg, transparent 95%, rgba(0, 255, 0, 0.2) 100%),
    linear-gradient(0deg, transparent 95%, rgba(0, 255, 0, 0.2) 100%),
    /* Add some retro patterns */
    repeating-linear-gradient(
      45deg,
      transparent,
      transparent 8px,
      rgba(255, 255, 255, 0.02) 8px,
      rgba(255, 255, 255, 0.02) 16px
    );
  background-size: 
    12px 12px,
    3px 3px,
    3px 3px,
    32px 32px;
  animation: pixelShift 6s ease-in-out infinite;
  opacity: 1;
}

/* Enhanced Screen Animations */
@keyframes screenFlicker {
  0%, 90%, 100% { 
    opacity: 1; 
    filter: brightness(1);
  }
  5% { 
    opacity: 0.8; 
    filter: brightness(1.2);
  }
  95% { 
    opacity: 0.9; 
    filter: brightness(0.8);
  }
  97% { 
    opacity: 1.1; 
    filter: brightness(1.3);
  }
}

@keyframes pixelShift {
  0%, 100% { 
    transform: translateX(0px) translateY(0px);
    opacity: 1;
    filter: hue-rotate(0deg);
  }
  25% { 
    transform: translateX(2px) translateY(0px);
    opacity: 0.8;
    filter: hue-rotate(90deg);
  }
  50% { 
    transform: translateX(0px) translateY(2px);
    opacity: 1.2;
    filter: hue-rotate(180deg);
  }
  75% { 
    transform: translateX(-2px) translateY(0px);
    opacity: 0.9;
    filter: hue-rotate(270deg);
  }
}

/* Enhanced CRT Screen Curvature Effect */
.about .container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  background: 
    radial-gradient(ellipse at center, transparent 30%, rgba(0, 0, 0, 0.3) 100%),
    /* Add some subtle noise */
    repeating-conic-gradient(from 0deg at 50% 50%, 
      transparent 0deg, 
      rgba(255, 255, 255, 0.01) 1deg, 
      transparent 2deg
    );
  pointer-events: none;
  animation: crtGlow 3s ease-in-out infinite alternate;
}

@keyframes crtGlow {
  0% { 
    filter: brightness(1) contrast(1); 
  }
  100% { 
    filter: brightness(1.05) contrast(1.1); 
  }
}

/* Enhanced RGB Chromatic Aberration */
.about .container::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  background: 
    linear-gradient(90deg, 
      rgba(255, 0, 0, 0.08) 0%,
      transparent 2%,
      transparent 98%,
      rgba(0, 0, 255, 0.08) 100%
    ),
    /* Add vertical color bands */
    linear-gradient(0deg,
      rgba(0, 255, 0, 0.04) 0%,
      transparent 3%,
      transparent 97%,
      rgba(255, 0, 255, 0.04) 100%
    );
  animation: chromaticShift 8s ease-in-out infinite;
  pointer-events: none;
  mix-blend-mode: overlay;
}

@keyframes chromaticShift {
  0%, 100% { 
    transform: translateX(0px) translateY(0px);
    filter: hue-rotate(0deg);
  }
  25% { 
    transform: translateX(1px) translateY(0px);
    filter: hue-rotate(90deg);
  }
  50% { 
    transform: translateX(0px) translateY(1px);
    filter: hue-rotate(180deg);
  }
  75% { 
    transform: translateX(-1px) translateY(0px);
    filter: hue-rotate(270deg);
  }
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

.image-placeholder {
  width: 100%;
  height: 400px;
  background: #000;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
  border: 3px solid #fff;
  box-shadow: 
    inset 0 0 20px rgba(0, 255, 0, 0.1),
    0 0 20px rgba(255, 255, 255, 0.1);
  /* Add retro screen effect */
  background: 
    repeating-linear-gradient(
      0deg,
      transparent 0px,
      transparent 1px,
      rgba(0, 255, 0, 0.03) 1px,
      rgba(0, 255, 0, 0.03) 2px
    ),
    #000;
}

.code-animation {
  background: #000;
  padding: 2rem 2.5rem 3rem 2rem;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  font-size: 0.7rem;
  color: #00ff00;
  width: 90%;
  border: 2px solid #00ff00;
  position: relative;
  line-height: 1.8;
  text-shadow: 0 0 5px rgba(0, 255, 0, 0.5);
  box-sizing: border-box;
  /* Add terminal-like styling */
  box-shadow: 
    inset 0 0 10px rgba(0, 255, 0, 0.1),
    0 0 15px rgba(0, 255, 0, 0.2);
  animation: terminalGlow 3s ease-in-out infinite alternate;
}

/* Add blinking cursor */
.code-animation::after {
  content: '█';
  color: #00ff00;
  animation: blink 1s infinite;
  position: absolute;
  bottom: 1rem;
  right: 1rem;
}

.code-line {
  opacity: 0;
  animation: typeIn 0.8s ease forwards;
  margin-bottom: 0.8rem;
  white-space: pre;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
  text-shadow: 0 0 3px rgba(0, 255, 0, 0.7);
  position: relative;
  word-wrap: break-word;
  overflow-wrap: break-word;
  max-width: 100%;
}

/* Enhanced syntax highlighting for 8-bit theme */
.code-line:nth-child(1) { 
  color: #00ff00; 
  font-weight: bold;
}
.code-line:nth-child(2) { 
  color: #ffff00; 
  padding-left: 0.8rem; 
  text-shadow: 0 0 3px rgba(255, 255, 0, 0.5);
}
.code-line:nth-child(3) { 
  color: #ff00ff; 
  padding-left: 0.8rem; 
  text-shadow: 0 0 3px rgba(255, 0, 255, 0.5);
}
.code-line:nth-child(4) { 
  color: #00ffff; 
  padding-left: 0.8rem; 
  text-shadow: 0 0 3px rgba(0, 255, 255, 0.5);
}
.code-line:nth-child(5) { 
  color: #ff8800; 
  padding-left: 0.8rem; 
  text-shadow: 0 0 3px rgba(255, 136, 0, 0.5);
}
.code-line:nth-child(6) { 
  color: #8800ff; 
  padding-left: 0.8rem; 
  text-shadow: 0 0 3px rgba(136, 0, 255, 0.5);
}
.code-line:nth-child(7) { 
  color: #00ff00; 
  font-weight: bold;
}

@keyframes typeIn {
  from {
    opacity: 0;
    transform: translateX(-20px);
    filter: blur(2px);
  }
  50% {
    filter: blur(1px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
    filter: blur(0px);
  }
}

/* 8-bit Scroll Animations */
.pixel-glitch-in {
  opacity: 1; /* Changed from 0 to 1 to make title always visible */
  transform: translateY(0); /* Changed from translateY(-20px) to 0 */
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

/* Enhanced hover effects */
.text-block.animate:hover {
  animation: pixelTextGlow 0.5s ease-in-out;
}

.pixel-stat-bounce.animate:hover {
  animation: pixelStatWiggle 0.6s ease-in-out;
}

@keyframes pixelTextGlow {
  0%, 100% { text-shadow: 0 0 5px rgba(255, 255, 255, 0.2); }
  50% { text-shadow: 0 0 15px rgba(0, 255, 255, 0.4), 0 0 25px rgba(0, 255, 255, 0.2); }
}

@keyframes pixelStatWiggle {
  0%, 100% { transform: rotate(0deg) scale(1); }
  25% { transform: rotate(-2deg) scale(1.02); }
  75% { transform: rotate(2deg) scale(1.02); }
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
  
  .image-placeholder {
    height: 300px;
    margin-top: 1rem;
  }
  
  .code-animation {
    font-size: 0.55rem;
    padding: 1.5rem 1.5rem 2rem 1.2rem;
    line-height: 1.6;
    width: 95%;
  }
  
  .code-line {
    margin-bottom: 0.6rem;
    word-break: break-word;
  }
  
  .code-line:nth-child(n+2) {
    padding-left: 0.6rem;
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
  
  .image-placeholder {
    height: 250px;
  }
  
  .code-animation {
    font-size: 0.5rem;
    padding: 1.2rem 1rem 1.5rem 1rem;
    line-height: 1.5;
    width: 98%;
  }
  
  .code-line {
    margin-bottom: 0.5rem;
  }
  
  .code-line:nth-child(n+2) {
    padding-left: 0.4rem;
  }
}

/* Content positioning above Tetris blocks */
.about .container {
  position: relative;
  z-index: 1;
}

/* Add 8-bit terminal animations */
@keyframes terminalGlow {
  0% { 
    box-shadow: 
      inset 0 0 10px rgba(0, 255, 0, 0.1),
      0 0 15px rgba(0, 255, 0, 0.2);
  }
  100% { 
    box-shadow: 
      inset 0 0 15px rgba(0, 255, 0, 0.2),
      0 0 25px rgba(0, 255, 0, 0.3);
  }
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}
</style>
