<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="container">
      <div class="nav-content">        <div class="logo">
          <h2 class="logo-text">
            <span class="glitch-char">S</span><span class="glitch-char">L</span>
          </h2>
        </div>        <ul class="nav-links" :class="{ 'nav-active': mobileMenuOpen }">
          <li>
            <a href="#home" @click="closeMobileMenu" class="nav-item" title="Go to Home">
              <i class="pixelart-icons-font-home nav-icon"></i>
              <span class="nav-text">Home</span>
            </a>
          </li>
          <li>
            <a href="#about" @click="closeMobileMenu" class="nav-item" title="Learn About Me">
              <i class="pixelart-icons-font-user nav-icon"></i>
              <span class="nav-text">About</span>
            </a>
          </li>
          <li>
            <a href="#skills" @click="closeMobileMenu" class="nav-item" title="View My Skills">
              <i class="pixelart-icons-font-trophy nav-icon"></i>
              <span class="nav-text">Skills</span>
            </a>
          </li>
          <li>
            <a href="#projects" @click="closeMobileMenu" class="nav-item" title="Explore My Projects">
              <i class="pixelart-icons-font-briefcase nav-icon"></i>
              <span class="nav-text">Projects</span>
            </a>
          </li>
          <li>
            <a href="#contact" @click="closeMobileMenu" class="nav-item" title="Get In Touch">
              <i class="pixelart-icons-font-mail nav-icon"></i>
              <span class="nav-text">Contact</span>
            </a>
          </li>
        </ul>
        <div class="hamburger" @click="toggleMobileMenu" :class="{ 'active': mobileMenuOpen }">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navigation',
  data() {
    return {
      isScrolled: false,
      mobileMenuOpen: false
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50
    },
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen
    },
    closeMobileMenu() {
      this.mobileMenuOpen = false
    }
  }
}
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
  border-bottom: 1px solid #fff;
}

.navbar-scrolled {
  background: rgba(0, 0, 0, 0.98);
  box-shadow: 0 1px 0 rgba(255, 255, 255, 0.1);
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
}

.logo-text {
  color: #fff;
  font-weight: 700;
  font-size: 1.8rem;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.logo .glitch-char {
  display: inline-block;
  transition: all 0.1s ease;
}

.logo .glitch-char:nth-child(1) {
  animation: logoGlitch 8s infinite;
  animation-delay: 0s;
}

.logo .glitch-char:nth-child(2) {
  animation: logoGlitch 10s infinite;
  animation-delay: 4s;
}

@keyframes logoGlitch {
  0%, 98%, 100% {
    transform: translateX(0);
    color: #fff;
    text-shadow: none;
  }
  99% {
    transform: translateX(1px);
    color: #0f0;
    text-shadow: -1px 0 rgba(255, 0, 0, 0.5);
  }
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-item {
  text-decoration: none;
  color: #fff;
  font-weight: 400;
  transition: all 0.3s ease;
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.7rem;
  padding: 0.7rem 0.8rem;
  border: 1px solid transparent;
  font-family: 'Space Mono', monospace;
}

.nav-item:hover {
  color: #fff;
  border-color: #fff;
  background: transparent;
}

.nav-icon {
  font-size: 1.1rem;
  min-width: 18px;
}

.nav-text {
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Tooltip styles */
.nav-item[title]:hover::before {
  content: attr(title);
  position: absolute;
  bottom: -65px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.95);
  color: #fff;
  padding: 0.6rem 0.8rem;
  border: 1px solid #fff;
  font-size: 0.7rem;
  white-space: nowrap;
  z-index: 1001;
  font-family: 'Space Mono', monospace;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.nav-item[title]:hover::after {
  content: '';
  position: absolute;
  bottom: -25px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-bottom: 6px solid #fff;
  z-index: 1002;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
  gap: 3px;
}

.hamburger span {
  width: 25px;
  height: 2px;
  background: #fff;
  transition: all 0.3s ease;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -6px);
}

@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
    .nav-links {
    position: fixed;
    top: 70px;
    right: -100%;
    width: 100%;
    height: calc(100vh - 70px);
    background: rgba(0, 0, 0, 0.98);
    backdrop-filter: blur(10px);
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    padding-top: 2rem;
    transition: right 0.3s ease;
  }
  
  .nav-links.nav-active {
    right: 0;
  }
  
  .nav-links li {
    margin: 1rem 0;
  }
  
  .nav-item {
    font-size: 1.2rem;
    padding: 1rem 2rem;
    border: 1px solid #333;
    gap: 1rem;
  }
  
  .nav-item:hover {
    border-color: #fff;
  }
  
  .nav-icon {
    font-size: 1.2rem;
  }
  
  .nav-text {
    font-size: 1rem;
  }
  
  /* Hide tooltips on mobile */
  .nav-item[title]:hover::before,
  .nav-item[title]:hover::after {
    display: none;
  }
}
</style>
