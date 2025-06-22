<template>
  <section id="contact" class="contact section">
    <div class="container">      <div class="section-header" ref="sectionHeader">
        <h2 class="section-title glitch-effect pixel-slide-down">Let's Work Together</h2>
        <div class="section-line pixel-expand"></div>
        <p class="section-description pixel-fade-up">
          Ready to bring your ideas to life? Let's discuss your next project!
        </p>
      </div>
        <div class="contact-content">
        <div class="contact-info">          <div class="info-card pixel-bounce-in" ref="infoCard1">
            <div class="info-icon">
              <i class="pixelart-icons-font-mail"></i>
            </div>
            <div class="info-details">
              <h3>Email Me</h3>              <p>sirlaudato@email.com</p>
              <a href="mailto:sir.laudato@email.com" class="info-link">Send Email</a>
            </div>
          </div>
          
          <div class="info-card pixel-bounce-in" ref="infoCard2">
            <div class="info-icon">
              <i class="pixelart-icons-font-deskphone"></i>
            </div>
            <div class="info-details">
              <h3>Call Me</h3>
              <p>+63 961 127 8650</p>
              <a href="tel:+15551234567" class="info-link">Call Now</a>
            </div>
          </div>
          
          <div class="info-card pixel-bounce-in" ref="infoCard3">
            <div class="info-icon">
              <i class="pixelart-icons-font-map"></i>
            </div>
            <div class="info-details">
              <h3>Location</h3>
              <p>Imus, Cavite</p>
              <span class="info-link">Available Remotely</span>
            </div>
          </div>
            <div class="social-links pixel-scale-up" ref="socialLinks">
            <h3 class="glitch-effect">Connect With Me</h3>            <div class="social-icons">
              <a href="#" class="social-icon pixel-pop" title="LinkedIn">
                <i class="pixelart-icons-font-briefcase"></i>
              </a>
              <a href="#" class="social-icon pixel-pop" title="GitHub">
                <i class="pixelart-icons-font-github"></i>
              </a>
              <a href="#" class="social-icon pixel-pop" title="Twitter">
                <i class="pixelart-icons-font-message"></i>
              </a>
              <a href="#" class="social-icon pixel-pop" title="Dribbble">
                <i class="pixelart-icons-font-colors-swatch"></i>
              </a>
            </div>
          </div>
        </div>        <div class="contact-form pixel-slide-left" ref="contactForm">
          <form @submit.prevent="submitForm">
            <div class="form-row">
              <div class="form-group">
                <label for="name">Full Name</label>                <input 
                  type="text" 
                  id="name" 
                  v-model="form.name"
                  :class="{ error: errors.name }"
                  placeholder="Your full name"
                  required
                >
                <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
              </div>
              
              <div class="form-group">
                <label for="email">Email Address</label>                <input 
                  type="email" 
                  id="email" 
                  v-model="form.email"
                  :class="{ error: errors.email }"
                  placeholder="your.email@example.com"
                  required
                >
                <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
              </div>
            </div>
            
            <div class="form-group">
              <label for="subject">Subject</label>              <input 
                type="text" 
                id="subject" 
                v-model="form.subject"
                :class="{ error: errors.subject }"
                placeholder="What's this about?"
                required
              >
              <span v-if="errors.subject" class="error-message">{{ errors.subject }}</span>
            </div>
            
            <div class="form-group">
              <label for="message">Message</label>              <textarea 
                id="message" 
                v-model="form.message"
                :class="{ error: errors.message }"
                placeholder="Tell me about your project..."
                rows="6"
                required
              ></textarea>
              <span v-if="errors.message" class="error-message">{{ errors.message }}</span>
            </div>
            
            <button type="submit" class="btn btn-primary btn-full" :disabled="isSubmitting">
              <span v-if="!isSubmitting">Send Message</span>
              <span v-else>Sending...</span>
            </button>
            
            <div v-if="submitMessage" class="submit-message" :class="submitStatus">
              {{ submitMessage }}
            </div>
          </form>
        </div>
      </div>
    </div>
      <footer class="footer pixel-fade-up" ref="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-left">
            <p>&copy; 2025 Sir Laudato. All rights reserved.</p>
          </div>          <div class="footer-right">
            <p>Built with <i class="pixelart-icons-font-heart pixel-heart-beat"></i> using Vue.js</p>
          </div>
        </div>
      </div>
    </footer>
  </section>
</template>

<script>
import emailjs from '@emailjs/browser'

export default {
  name: 'ContactSection',
  data() {
    return {
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      errors: {},
      isSubmitting: false,
      submitMessage: '',
      submitStatus: '',
      observer: null
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
      // Create intersection observer for scroll animations
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate')
            
            // Stagger social icons animation
            if (entry.target === this.$refs.socialLinks) {
              const icons = entry.target.querySelectorAll('.social-icon')
              icons.forEach((icon, index) => {
                setTimeout(() => {
                  icon.classList.add('animate')
                }, index * 100)
              })
            }
            
            // Stop observing once animated
            this.observer.unobserve(entry.target)
          }
        })
      }, {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
      })      // Observe elements
      const elementsToObserve = [
        this.$refs.sectionHeader,
        this.$refs.infoCard1,
        this.$refs.infoCard2,
        this.$refs.infoCard3,
        this.$refs.socialLinks,
        this.$refs.contactForm,
        this.$refs.footer
      ]

      elementsToObserve.forEach(el => {
        if (el) {
          this.observer.observe(el)
        }
      })
    },
    validateForm() {
      this.errors = {}
      
      if (!this.form.name.trim()) {
        this.errors.name = 'Name is required'
      }
      
      if (!this.form.email.trim()) {
        this.errors.email = 'Email is required'
      } else if (!this.isValidEmail(this.form.email)) {
        this.errors.email = 'Please enter a valid email'
      }
      
      if (!this.form.subject.trim()) {
        this.errors.subject = 'Subject is required'
      }
      
      if (!this.form.message.trim()) {
        this.errors.message = 'Message is required'
      } else if (this.form.message.trim().length < 10) {
        this.errors.message = 'Message must be at least 10 characters long'
      }
      
      return Object.keys(this.errors).length === 0
    },
    
    isValidEmail(email) {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return emailRegex.test(email)
    },    async submitForm() {
      if (!this.validateForm()) {
        return
      }
      
      this.isSubmitting = true
      this.submitMessage = ''
      
      try {
        // Method 1: Try EmailJS first (works without server setup)
        await this.sendEmailWithEmailJS()
        
      } catch (emailjsError) {
        console.log('EmailJS failed, trying server API...', emailjsError)
        
        try {
          // Method 2: Fallback to server API
          await this.sendEmailWithAPI()
          
        } catch (apiError) {
          console.error('Both email methods failed:', { emailjsError, apiError })
          this.submitMessage = 'Oops! Something went wrong. Please try again later or email me directly at sirlaudato@gmail.com'
          this.submitStatus = 'error'
          
          setTimeout(() => {
            this.submitMessage = ''
          }, 8000)
        }
      }
      
      this.isSubmitting = false
    },    async sendEmailWithEmailJS() {
      // Initialize EmailJS with your credentials
      const serviceID = 'service_g2hgemy'
      const templateID = 'template_lelcbjt'
      const publicKey = 'bvS05RCV3uO769JZPiQOx'

      const templateParams = {
        from_name: this.form.name,
        from_email: this.form.email,
        title: this.form.subject, // Maps to {{title}} in your template
        message: this.form.message
      }

      await emailjs.send(serviceID, templateID, templateParams, publicKey)
      
      // Reset form on success
      this.form = {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
      
      this.submitMessage = 'Thank you! Your message has been sent successfully to sirlaudato@gmail.com'
      this.submitStatus = 'success'
      
      setTimeout(() => {
        this.submitMessage = ''
      }, 7000)
    },

    async sendEmailWithAPI() {
      // Send email via Vercel API route
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name: this.form.name,
          email: this.form.email,
          subject: this.form.subject,
          message: this.form.message
        })
      })
      
      const data = await response.json()
      
      if (response.ok && data.success) {
        // Reset form
        this.form = {
          name: '',
          email: '',
          subject: '',
          message: ''
        }
        
        this.submitMessage = 'Thank you! Your message has been sent successfully to sirlaudato@gmail.com'
        this.submitStatus = 'success'
        
        setTimeout(() => {
          this.submitMessage = ''
        }, 7000)
      } else {
        throw new Error(data.message || 'Failed to send message')
      }
    }
  }
}
</script>

<style scoped>
/* Hide honeypot field */
.hidden {
  display: none;
}

.contact {
  background: #000;
  color: #fff;
  position: relative;
  overflow: hidden;
  padding-bottom: 0; /* Remove bottom padding since we have a footer */
}

.contact::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    repeating-linear-gradient(
      90deg,
      transparent,
      transparent 2px,
      rgba(255, 255, 255, 0.03) 2px,
      rgba(255, 255, 255, 0.03) 4px
    ),
    repeating-linear-gradient(
      180deg,
      transparent,
      transparent 2px,
      rgba(255, 255, 255, 0.03) 2px,
      rgba(255, 255, 255, 0.03) 4px
    );
  pointer-events: none;
}

.contact::after {
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
    rgba(255, 255, 255, 0.05) 2px,
    rgba(255, 255, 255, 0.05) 4px
  );
  animation: scanlines 2s linear infinite;
  pointer-events: none;
}

@keyframes scanlines {
  0% { transform: translateY(0); }
  100% { transform: translateY(4px); }
}

/* 8-bit Scroll Animations */
.pixel-slide-down {
  opacity: 1; /* Changed from 0 to 1 to make title always visible */
  transform: translateY(0) scaleY(1); /* Changed to default visible state */
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-slide-down.animate {
  opacity: 1;
  transform: translateY(0) scaleY(1);
  animation: pixelGlitchIn 0.1s ease-in-out 0.4s;
}

.pixel-expand {
  width: 0;
  transition: width 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-expand.animate {
  width: 120px;
  animation: pixelFlicker 0.3s ease-in-out 0.6s;
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

.pixel-bounce-in {
  opacity: 0;
  transform: scale(0.3) translateY(50px);
  transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-bounce-in.animate {
  opacity: 1;
  transform: scale(1) translateY(0);
}

.pixel-scale-up {
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-scale-up.animate {
  opacity: 1;
  transform: scale(1);
  animation: pixelPulse 0.4s ease-in-out 0.3s;
}

.pixel-slide-left {
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.7s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.pixel-slide-left.animate {
  opacity: 1;
  transform: translateX(0);
}

.pixel-pop {
  transform: scale(1);
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.pixel-pop.animate {
  animation: pixelPop 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

@keyframes pixelGlitchIn {
  0% { transform: translateX(0); }
  25% { transform: translateX(-2px); filter: hue-rotate(90deg); }
  50% { transform: translateX(2px); filter: hue-rotate(180deg); }
  75% { transform: translateX(-1px); filter: hue-rotate(270deg); }
  100% { transform: translateX(0); filter: hue-rotate(0deg); }
}

@keyframes pixelFlicker {
  0%, 100% { opacity: 1; box-shadow: 0 0 10px rgba(255, 255, 255, 0.5); }
  25% { opacity: 0.8; box-shadow: 0 0 20px rgba(0, 255, 0, 0.6); }
  50% { opacity: 1; box-shadow: 0 0 15px rgba(255, 0, 255, 0.6); }
  75% { opacity: 0.9; box-shadow: 0 0 25px rgba(0, 255, 255, 0.6); }
}

@keyframes pixelPulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); box-shadow: 0 0 20px rgba(255, 255, 255, 0.3); }
  100% { transform: scale(1); }
}

@keyframes pixelPop {
  0% { transform: scale(1); }
  30% { transform: scale(1.2) rotate(5deg); }
  60% { transform: scale(0.9) rotate(-3deg); }
  100% { transform: scale(1) rotate(0deg); }
}

/* Staggered info card animations */
.info-card:nth-child(1).animate {
  transition-delay: 0.1s;
}

.info-card:nth-child(2).animate {
  transition-delay: 0.2s;
}

.info-card:nth-child(3).animate {
  transition-delay: 0.3s;
}

/* Enhanced hover effects for animated elements */
.info-card.animate:hover {
  animation: pixelShake 0.5s ease-in-out;
}

.social-icon.animate:hover {
  animation: pixelBounce 0.4s ease-in-out;
}

@keyframes pixelShake {
  0%, 100% { transform: translateY(-5px) translateX(0); }
  25% { transform: translateY(-5px) translateX(-2px); }
  75% { transform: translateY(-5px) translateX(2px); }
}

@keyframes pixelBounce {
  0%, 100% { transform: translateY(-3px) scale(1); }
  50% { transform: translateY(-8px) scale(1.1); }
}

/* Heart beat animation */
.pixel-heart-beat {
  animation: heartBeat 2s ease-in-out infinite;
  color: #ff4757;
  display: inline-block;
}

@keyframes heartBeat {
  0%, 100% { transform: scale(1); }
  25% { transform: scale(1.1); }
  50% { transform: scale(1.2); }
  75% { transform: scale(1.1); }
}

/* Form element animations */
.contact-form.animate .form-group {
  animation: pixelSlideUp 0.6s ease-out forwards;
  opacity: 0;
  transform: translateY(30px);
}

.contact-form.animate .form-group:nth-child(1) { animation-delay: 0.1s; }
.contact-form.animate .form-group:nth-child(2) { animation-delay: 0.2s; }
.contact-form.animate .form-group:nth-child(3) { animation-delay: 0.3s; }
.contact-form.animate .form-group:nth-child(4) { animation-delay: 0.4s; }
.contact-form.animate .btn-full { animation-delay: 0.5s; }

@keyframes pixelSlideUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Add some particle-like effects */
.section-header.animate::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 80%, rgba(255, 255, 255, 0.1) 1px, transparent 1px),
    radial-gradient(circle at 80% 20%, rgba(0, 255, 0, 0.1) 1px, transparent 1px),
    radial-gradient(circle at 40% 40%, rgba(255, 0, 255, 0.1) 1px, transparent 1px);
  background-size: 50px 50px, 30px 30px, 40px 40px;
  animation: pixelFloat 10s linear infinite;
  pointer-events: none;
  z-index: -1;
}

@keyframes pixelFloat {
  0% { transform: translateY(0px) translateX(0px); }
  33% { transform: translateY(-10px) translateX(5px); }
  66% { transform: translateY(5px) translateX(-3px); }
  100% { transform: translateY(0px) translateX(0px); }
}

/* Glitch Effect */
.glitch-effect {
  position: relative;
  animation: glitch 2s infinite;
}

.glitch-effect::before,
.glitch-effect::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #000;
}

.glitch-effect::before {
  animation: glitch-1 0.5s infinite;
  color: #00ff00;
  z-index: -1;
}

.glitch-effect::after {
  animation: glitch-2 0.5s infinite;
  color: #ff0000;
  z-index: -2;
}

@keyframes glitch {
  0%, 100% { transform: translate(0); }
  20% { transform: translate(-2px, 2px); }
  40% { transform: translate(-2px, -2px); }
  60% { transform: translate(2px, 2px); }
  80% { transform: translate(2px, -2px); }
}

@keyframes glitch-1 {
  0%, 100% { transform: translate(0); }
  20% { transform: translate(-1px, -1px); }
  40% { transform: translate(-1px, 1px); }
  60% { transform: translate(1px, -1px); }
  80% { transform: translate(1px, 1px); }
}

@keyframes glitch-2 {
  0%, 100% { transform: translate(0); }
  20% { transform: translate(1px, 1px); }
  40% { transform: translate(1px, -1px); }
  60% { transform: translate(-1px, 1px); }
  80% { transform: translate(-1px, -1px); }
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
  position: relative;
  z-index: 1;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 400;
  margin-bottom: 1rem;
  font-family: 'Press Start 2P', monospace;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #fff;
  text-shadow: 2px 2px 0px #333;
  image-rendering: pixelated;
}

.section-line {
  width: 120px;
  height: 4px;
  background: #fff;
  margin: 0 auto 1.5rem;
  image-rendering: pixelated;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
}

.section-description {
  font-size: 1rem;
  opacity: 0.9;
  max-width: 600px;
  margin: 0 auto;
  font-family: 'Space Mono', monospace;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 4rem;
  align-items: start;
  position: relative;
  z-index: 1;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.info-card {
  background: rgba(255, 255, 255, 0.1);
  border: 3px solid #fff;
  border-style: solid;
  border-image: url("data:image/svg+xml,%3csvg width='100' height='100' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M0 0h100v100H0z' fill='none' stroke='%23fff' stroke-width='3'/%3e%3c/svg%3e") 3;
  padding: 2rem;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  transition: all 0.3s ease;
  image-rendering: pixelated;
  position: relative;
}

.info-card::before {
  content: '';
  position: absolute;
  top: -3px;
  left: -3px;
  right: -3px;
  bottom: -3px;
  background: 
    linear-gradient(45deg, 
      transparent 30%, 
      rgba(255, 255, 255, 0.1) 50%, 
      transparent 70%
    );
  z-index: -1;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.info-card:hover {
  transform: translateY(-5px);
  border-color: #fff;
  box-shadow: 0 8px 25px rgba(255, 255, 255, 0.2);
}

.info-card:hover::before {
  opacity: 1;
}

.info-icon {
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid #fff;
  image-rendering: pixelated;
}

.info-details h3 {
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
  font-weight: 400;
  font-family: 'Press Start 2P', monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
  image-rendering: pixelated;
}

.info-details p {
  opacity: 0.9;
  margin-bottom: 0.5rem;
  font-family: 'Space Mono', monospace;
}

.info-link {
  color: #e8eaf6;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  font-family: 'Space Mono', monospace;
}

.info-link:hover {
  text-decoration: underline;
}

.social-links {
  background: rgba(255, 255, 255, 0.1);
  border: 3px solid #fff;
  border-image: url("data:image/svg+xml,%3csvg width='100' height='100' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M0 0h100v100H0z' fill='none' stroke='%23fff' stroke-width='3'/%3e%3c/svg%3e") 3;
  padding: 2rem;
  text-align: center;
  image-rendering: pixelated;
}

.social-links h3 {
  margin-bottom: 1.5rem;
  font-size: 0.8rem;
  font-family: 'Press Start 2P', monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 400;
  image-rendering: pixelated;
}

.social-icons {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.social-icon {
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid #fff;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  font-size: 1.2rem;
  transition: all 0.3s ease;
  image-rendering: pixelated;
}

.social-icon:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: translateY(-3px);
  border-color: #fff;
  box-shadow: 0 6px 20px rgba(255, 255, 255, 0.3);
}

.contact-form {
  background: rgba(255, 255, 255, 0.95);
  border: 4px solid #000;
  border-image: url("data:image/svg+xml,%3csvg width='100' height='100' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M0 0h100v100H0z' fill='none' stroke='%23000' stroke-width='4'/%3e%3c/svg%3e") 4;
  padding: 3rem;
  color: #000;
  position: relative;
  image-rendering: pixelated;
}

.contact-form::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    repeating-linear-gradient(
      45deg,
      transparent,
      transparent 10px,
      rgba(0, 0, 0, 0.02) 10px,
      rgba(0, 0, 0, 0.02) 20px
    );
  pointer-events: none;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 400;
  color: #000;
  font-family: 'Press Start 2P', monospace;
  text-transform: uppercase;
  font-size: 0.6rem;
  letter-spacing: 1px;
  image-rendering: pixelated;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 3px solid #000;
  background: #fff;
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: 'Space Mono', monospace;
  image-rendering: pixelated;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #333;
  box-shadow: 0 0 0 2px rgba(0, 0, 0, 0.2);
}

.form-group input.error,
.form-group textarea.error {
  border-color: #dc3545;
  box-shadow: 0 0 0 2px rgba(220, 53, 69, 0.2);
}

.error-message {
  color: #dc3545;
  font-size: 0.85rem;
  margin-top: 0.25rem;
  display: block;
  font-family: 'Space Mono', monospace;
}

.btn-full {
  width: 100%;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  font-family: 'Press Start 2P', monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
  background: #000;
  color: #fff;
  border: 3px solid #000;
  transition: all 0.3s ease;
  cursor: pointer;
  image-rendering: pixelated;
}

.btn-full:hover:not(:disabled) {
  background: #fff;
  color: #000;
  border-color: #000;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
}

.btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border: 2px solid transparent;
  text-align: center;
  font-weight: 500;
  font-family: 'Space Mono', monospace;
  image-rendering: pixelated;
}

.submit-message.success {
  background: #d4edda;
  color: #155724;
  border-color: #c3e6cb;
}

.submit-message.error {
  background: #f8d7da;
  color: #721c24;
  border-color: #f5c6cb;
}

.footer {
  background: rgba(0, 0, 0, 0.9);
  padding: 2rem 0;
  margin-top: 4rem;
  border-top: 3px solid #fff;
  position: relative;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    repeating-linear-gradient(
      90deg,
      transparent,
      transparent 8px,
      rgba(255, 255, 255, 0.05) 8px,
      rgba(255, 255, 255, 0.05) 16px
    );
  pointer-events: none;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: rgba(255, 255, 255, 0.8);
  font-family: 'Press Start 2P', monospace;
  font-size: 0.6rem;
  position: relative;
  z-index: 1;
  image-rendering: pixelated;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 1.8rem;
    letter-spacing: 2px;
    line-height: 1.3;
    margin-bottom: 1rem;
  }
  
  .section-description {
    font-size: 0.9rem;
    padding: 0 1rem;
    line-height: 1.5;
  }
  
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
    padding: 0 1rem;
  }
  
  .contact-info {
    gap: 1.5rem;
  }
  
  .info-card {
    padding: 1.5rem;
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }
  
  .info-icon {
    margin: 0 auto;
  }
  
  .info-details h3 {
    font-size: 0.7rem;
    margin-bottom: 0.5rem;
  }
  
  .info-details p {
    font-size: 0.9rem;
    margin-bottom: 0.3rem;
  }
  
  .info-link {
    font-size: 0.8rem;
  }
  
  .social-links {
    padding: 1.5rem;
  }
  
  .social-links h3 {
    font-size: 0.7rem;
    margin-bottom: 1rem;
  }
  
  .social-icons {
    flex-wrap: wrap;
    gap: 0.8rem;
    justify-content: center;
  }
  
  .social-icon {
    width: 45px;
    height: 45px;
    font-size: 1.1rem;
  }
  
  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }
  
  .contact-form {
    padding: 2rem 1.5rem;
  }
  
  .form-group {
    margin-bottom: 1.2rem;
  }
  
  .form-group label {
    font-size: 0.5rem;
    margin-bottom: 0.4rem;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 0.6rem 0.8rem;
    font-size: 0.9rem;
  }
  
  .btn-full {
    font-size: 0.8rem;
    padding: 0.8rem 1.5rem;
  }
  
  .footer-content {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
    font-size: 0.5rem;
    line-height: 1.4;
  }
}

@media (max-width: 480px) {
  .section-title {
    font-size: 1.5rem;
    letter-spacing: 1px;
  }
  
  .section-description {
    font-size: 0.85rem;
    padding: 0 0.5rem;
  }
  
  .contact-content {
    padding: 0 0.5rem;
    gap: 1.5rem;
  }
  
  .info-card {
    padding: 1.2rem;
    gap: 0.8rem;
  }
  
  .info-icon {
    width: 40px;
    height: 40px;
    font-size: 1.2rem;
  }
  
  .info-details h3 {
    font-size: 0.65rem;
  }
  
  .info-details p {
    font-size: 0.85rem;
  }
  
  .info-link {
    font-size: 0.75rem;
  }
  
  .social-links {
    padding: 1.2rem;
  }
  
  .social-links h3 {
    font-size: 0.65rem;
  }
  
  .social-icons {
    gap: 0.6rem;
  }
  
  .social-icon {
    width: 40px;
    height: 40px;
    font-size: 1rem;
  }
  
  .contact-form {
    padding: 1.5rem 1rem;
  }
  
  .form-group label {
    font-size: 0.45rem;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 0.5rem 0.7rem;
    font-size: 0.85rem;
  }
  
  .btn-full {
    font-size: 0.7rem;
    padding: 0.7rem 1.2rem;
  }
  
  .footer-content {
    font-size: 0.45rem;
    gap: 0.8rem;
  }
}
</style>
