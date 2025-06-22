<template>
  <section id="home" class="hero">
    <div class="container">      <div class="hero-content">        <div class="hero-left">
          <div class="hero-text" ref="heroText">            <h1 class="hero-title">
              <span class="name glitch-text">
                <span class="glitch-char">S</span><span class="glitch-char">I</span><span class="glitch-char">R</span>
              </span>
              <span class="name glitch-text">
                <span class="glitch-char">L</span><span class="glitch-char">A</span><span class="glitch-char">U</span><span class="glitch-char">D</span><span class="glitch-char">A</span><span class="glitch-char">T</span><span class="glitch-char">O</span>
              </span>
              <span class="title glitch-text">
                <span class="glitch-char">F</span><span class="glitch-char">R</span><span class="glitch-char">O</span><span class="glitch-char">N</span><span class="glitch-char">T</span><span class="glitch-char">E</span><span class="glitch-char">N</span><span class="glitch-char">D</span>
                <span class="space">&nbsp;</span>
                <span class="glitch-char">D</span><span class="glitch-char">E</span><span class="glitch-char">V</span><span class="glitch-char">E</span><span class="glitch-char">L</span><span class="glitch-char">O</span><span class="glitch-char">P</span><span class="glitch-char">E</span><span class="glitch-char">R</span>
              </span>
            </h1><p class="hero-description glitch-description">
              <span class="glitch-word">Crafting</span> <span class="glitch-word">pixel-perfect,</span> <span class="glitch-word">functional</span> <span class="glitch-word">web</span> <span class="glitch-word">experiences.</span><br>
              <span class="glitch-word">Clean</span> <span class="glitch-word">code.</span> <span class="glitch-word">Minimal</span> <span class="glitch-word">design.</span> <span class="glitch-word">Maximum</span> <span class="glitch-word">impact.</span>
            </p>
            <div class="hero-buttons">
              <a href="#projects" class="btn btn-primary">VIEW WORK</a>
              <a href="#contact" class="btn btn-secondary">CONTACT</a>
            </div>
          </div>
        </div>
        <div class="hero-right">          <div class="game-container pixel-game-slide" ref="gameContainer"><div class="game-header">
              <h3 class="game-title glitch-text">
                <span class="glitch-char">P</span><span class="glitch-char">O</span><span class="glitch-char">N</span><span class="glitch-char">G</span>
                <span class="space">&nbsp;</span>
                <span class="glitch-char">G</span><span class="glitch-char">A</span><span class="glitch-char">M</span><span class="glitch-char">E</span>
              </h3>
              <div class="game-controls">
                <button v-if="!gameActive && !gameStarted" @click="startGame" class="game-btn">PLAY</button>
                <button v-if="gameActive" @click="pauseGame" class="game-btn">{{ gamePaused ? 'RESUME' : 'PAUSE' }}</button>
                <button v-if="gameActive || gameStarted" @click="cancelGame" class="game-btn cancel">CANCEL</button>
              </div>
            </div>
            <div class="game-stats">
              <div class="stat">
                <span class="stat-label">PLAYER</span>
                <span class="stat-value">{{ playerScore }}</span>
              </div>
              <div class="stat">
                <span class="stat-label">CPU</span>
                <span class="stat-value">{{ cpuScore }}</span>
              </div>
              <div class="stat">
                <span class="stat-label">SPEED</span>
                <span class="stat-value">{{ gameSpeed }}</span>
              </div>
            </div>
            <div class="game-board" ref="gameBoard" @keydown="handleKeyDown" @keyup="handleKeyUp" tabindex="0">
              <!-- Mobile Touch Controls -->
              <div v-if="gameActive && isMobile" class="mobile-controls">
                <button 
                  class="touch-btn touch-up" 
                  @touchstart="handleTouchStart('up')"
                  @touchend="handleTouchEnd('up')"
                  @mousedown="handleTouchStart('up')"
                  @mouseup="handleTouchEnd('up')"
                >
                  ↑
                </button>
                <button 
                  class="touch-btn touch-down" 
                  @touchstart="handleTouchStart('down')"
                  @touchend="handleTouchEnd('down')"
                  @mousedown="handleTouchStart('down')"
                  @mouseup="handleTouchEnd('down')"
                >
                  ↓
                </button>
              </div>

              <!-- Player Paddle -->
              <div 
                v-if="gameActive || gameStarted"
                class="paddle player-paddle" 
                :style="{ left: '20px', top: playerPaddle.y + 'px' }"
              >
                <div class="pixel-paddle"></div>
              </div>
              
              <!-- CPU Paddle -->
              <div 
                v-if="gameActive || gameStarted"
                class="paddle cpu-paddle" 
                :style="{ right: '20px', top: cpuPaddle.y + 'px' }"
              >
                <div class="pixel-paddle"></div>
              </div>
              
              <!-- Ball -->
              <div 
                v-if="gameActive || gameStarted"
                class="ball" 
                :style="{ left: ball.x + 'px', top: ball.y + 'px' }"
              >
                <div class="pixel-ball"></div>
              </div>
              
              <!-- Center Line -->
              <div v-if="gameActive || gameStarted" class="center-line">
                <div class="line-segment" v-for="i in 10" :key="i"></div>
              </div>
                <!-- Game Over Screen -->
              <div v-if="!gameActive && gameStarted && !gamePaused" class="game-overlay">
                <div class="game-over">
                  <h4>{{ gameWinner ? `${gameWinner.toUpperCase()} WINS!` : 'GAME OVER' }}</h4>
                  <p>FINAL SCORE: {{ playerScore }} - {{ cpuScore }}</p>
                  <button @click="startGame" class="game-btn">PLAY AGAIN</button>
                </div>
              </div>
              
              <!-- Pause Screen -->
              <div v-if="gamePaused" class="game-overlay pause-overlay">
                <div class="pause-screen">
                  <h4>PAUSED</h4>
                  <p>PRESS RESUME TO CONTINUE</p>
                </div>
              </div>
                <!-- Start Screen -->
              <div v-if="!gameActive && !gameStarted" class="game-overlay">
                <div class="start-screen">
                  <h4>CLASSIC PONG</h4>
                  <p v-if="!isMobile">USE ↑ ↓ TO MOVE PADDLE</p>
                  <p v-if="isMobile">USE TOUCH BUTTONS TO MOVE</p>
                  <p>FIRST TO 5 POINTS WINS</p>
                  <button @click="startGame" class="game-btn">START GAME</button>
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
  name: 'HeroSection',  data() {
    return {
      gameActive: false,
      gameStarted: false,
      gamePaused: false,
      gameWinner: null,
      playerScore: 0,
      cpuScore: 0,
      gameSpeed: 1,
        // Game board dimensions
      boardWidth: 400,
      boardHeight: 350,
      
      // Player paddle
      playerPaddle: {
        y: 100,
        width: 10,
        height: 50,
        speed: 4
      },
      
      // CPU paddle
      cpuPaddle: {
        y: 100,
        width: 10,
        height: 50,
        speed: 2.5
      },
      
      // Ball
      ball: {
        x: 200,
        y: 125,
        width: 8,
        height: 8,
        speedX: 3,
        speedY: 2
      },
        // Game mechanics
      keys: {},
      gameInterval: null,
      
      // Mobile support
      isMobile: false,
      touchControls: {
        up: false,
        down: false
      },
      
      // Game settings
      maxScore: 5,
      ballSpeedIncrease: 0.2,
      observer: null
    }
  },
  mounted() {
    this.detectMobile()
    this.setupKeyboardListeners()
    this.initScrollAnimations()
  },
    beforeUnmount() {
    this.cleanup()
    if (this.observer) {
      this.observer.disconnect()
    }
  },
    methods: {
    detectMobile() {
      this.isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) || 
                      window.innerWidth <= 768
    },

    handleTouchStart(direction) {
      if (!this.gameActive || this.gamePaused) return
      this.touchControls[direction] = true
    },

    handleTouchEnd(direction) {
      if (!this.gameActive || this.gamePaused) return
      this.touchControls[direction] = false
    },    setupKeyboardListeners() {
      window.addEventListener('keydown', this.handleKeyDown)
      window.addEventListener('keyup', this.handleKeyUp)
      window.addEventListener('resize', this.detectMobile)
    },
      initScrollAnimations() {
      // Add initial animation trigger for game container
      setTimeout(() => {
        if (this.$refs.gameContainer) {
          this.$refs.gameContainer.classList.add('animate')
        }
      }, 500) // Slight delay for initial load
    },handleKeyDown(event) {
      if (!this.gameActive || this.gamePaused) return
      
      // Prevent default behavior for arrow keys to stop page scrolling
      if (event.code === 'ArrowUp' || event.code === 'ArrowDown') {
        event.preventDefault()
      }
      
      this.keys[event.code] = true
    },
    
    handleKeyUp(event) {
      if (!this.gameActive || this.gamePaused) return
      
      // Prevent default behavior for arrow keys to stop page scrolling
      if (event.code === 'ArrowUp' || event.code === 'ArrowDown') {
        event.preventDefault()
      }
      
      this.keys[event.code] = false
    },
      startGame() {
      this.resetGame()
      this.gameActive = true
      this.gameStarted = true
      this.gamePaused = false
      this.gameWinner = null
      this.gameLoop()
    },
    
    pauseGame() {
      this.gamePaused = !this.gamePaused
      if (!this.gamePaused) {
        this.gameLoop()
      }
    },
    
    cancelGame() {
      this.gameActive = false
      this.gameStarted = false
      this.gamePaused = false
      this.cleanup()
      this.resetGame()
    },
      resetGame() {
      this.playerScore = 0
      this.cpuScore = 0
      this.gameSpeed = 1
      this.gameWinner = null
      
      // Reset paddle positions
      this.playerPaddle.y = (this.boardHeight - this.playerPaddle.height) / 2
      this.cpuPaddle.y = (this.boardHeight - this.cpuPaddle.height) / 2
      
      // Reset ball position and velocity
      this.ball.x = this.boardWidth / 2
      this.ball.y = this.boardHeight / 2
      this.ball.speedX = Math.random() > 0.5 ? 3 : -3
      this.ball.speedY = Math.random() * 4 - 2
      
      this.keys = {}
    },      updatePlayerPaddle() {
      // Handle keyboard controls
      const upPressed = this.keys['ArrowUp'] || this.touchControls.up
      const downPressed = this.keys['ArrowDown'] || this.touchControls.down
      
      if (upPressed && this.playerPaddle.y > 0) {
        this.playerPaddle.y -= this.playerPaddle.speed
      }
      if (downPressed && this.playerPaddle.y < this.boardHeight - this.playerPaddle.height) {
        this.playerPaddle.y += this.playerPaddle.speed
      }
    },

    updateCpuPaddle() {
      const paddleCenter = this.cpuPaddle.y + this.cpuPaddle.height / 2
      const ballCenter = this.ball.y + this.ball.height / 2
      
      if (paddleCenter < ballCenter - 10) {
        this.cpuPaddle.y += this.cpuPaddle.speed
      } else if (paddleCenter > ballCenter + 10) {
        this.cpuPaddle.y -= this.cpuPaddle.speed
      }
      
      // Keep CPU paddle within bounds
      if (this.cpuPaddle.y < 0) this.cpuPaddle.y = 0
      if (this.cpuPaddle.y > this.boardHeight - this.cpuPaddle.height) {
        this.cpuPaddle.y = this.boardHeight - this.cpuPaddle.height
      }
    },

    updateBall() {
      this.ball.x += this.ball.speedX
      this.ball.y += this.ball.speedY
      
      // Ball collision with top and bottom walls
      if (this.ball.y <= 0 || this.ball.y >= this.boardHeight - this.ball.height) {
        this.ball.speedY = -this.ball.speedY
      }
      
      // Ball goes out of bounds (scoring)
      if (this.ball.x < 0) {
        this.cpuScore++
        this.resetBall()
      } else if (this.ball.x > this.boardWidth) {
        this.playerScore++
        this.resetBall()
      }
    },

    resetBall() {
      this.ball.x = this.boardWidth / 2
      this.ball.y = this.boardHeight / 2
      this.ball.speedX = Math.random() > 0.5 ? 3 : -3
      this.ball.speedY = Math.random() * 4 - 2
      
      // Increase game speed slightly
      this.gameSpeed += 0.1
      if (Math.abs(this.ball.speedX) < 5) {
        this.ball.speedX *= 1.05
      }
    },
      gameLoop() {
      if (!this.gameActive || this.gamePaused) return
      
      this.updatePlayerPaddle()
      this.updateCpuPaddle()
      this.updateBall()
      this.checkCollisions()
      this.checkGameConditions()
      
      requestAnimationFrame(this.gameLoop)
    },    
    checkCollisions() {
      // Ball collision with player paddle
      if (this.ball.x <= 30 && 
          this.ball.x >= 20 &&
          this.ball.y >= this.playerPaddle.y &&
          this.ball.y <= this.playerPaddle.y + this.playerPaddle.height) {
        this.ball.speedX = Math.abs(this.ball.speedX)
        
        // Add some angle based on where the ball hits the paddle
        const hitPos = (this.ball.y - this.playerPaddle.y) / this.playerPaddle.height
        this.ball.speedY = (hitPos - 0.5) * 6
      }
      
      // Ball collision with CPU paddle
      if (this.ball.x >= this.boardWidth - 30 &&
          this.ball.x <= this.boardWidth - 20 &&
          this.ball.y >= this.cpuPaddle.y &&
          this.ball.y <= this.cpuPaddle.y + this.cpuPaddle.height) {
        this.ball.speedX = -Math.abs(this.ball.speedX)
        
        // Add some angle based on where the ball hits the paddle
        const hitPos = (this.ball.y - this.cpuPaddle.y) / this.cpuPaddle.height
        this.ball.speedY = (hitPos - 0.5) * 6
      }
    },

    checkGameConditions() {
      if (this.playerScore >= this.maxScore) {
        this.endGame('Player')
      } else if (this.cpuScore >= this.maxScore) {
        this.endGame('CPU')
      }
    },

    endGame(winner) {
      this.gameActive = false
      this.gameWinner = winner
      this.cleanup()    },
      cleanup() {
      if (this.gameInterval) {
        clearInterval(this.gameInterval)
        this.gameInterval = null
      }
      
      // Remove event listeners
      window.removeEventListener('keydown', this.handleKeyDown)
      window.removeEventListener('keyup', this.handleKeyUp)
      window.removeEventListener('resize', this.detectMobile)
    }
  }
}
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: #000;
  color: #fff;
  position: relative;
  border-bottom: 1px solid #fff;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 1;
}

.hero-text {
  animation: fadeInUp 1s ease forwards;
}

.hero-title {
  font-size: 4rem;
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.name {
  font-size: 4.5rem;
  color: #fff;
  margin-bottom: 0.5rem;
  letter-spacing: -2px;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.title {
  font-size: 1.5rem;
  color: #999;
  font-weight: 400;
  letter-spacing: 2px;
  text-transform: uppercase;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

/* Glitch Effects */
.glitch-text {
  position: relative;
  display: inline-block;
}

.glitch-char {
  display: inline-block;
  position: relative;
  transition: all 0.1s ease;
}

.glitch-char:nth-child(odd):hover {
  animation: glitchOdd 0.6s infinite;
}

.glitch-char:nth-child(even):hover {
  animation: glitchEven 0.8s infinite;
}

/* Random glitch triggers */
.glitch-char:nth-child(3n) {
  animation: subtleGlitch 4s infinite;
  animation-delay: 0s;
}

.glitch-char:nth-child(5n) {
  animation: subtleGlitch 6s infinite;
  animation-delay: 2s;
}

.glitch-char:nth-child(7n) {
  animation: subtleGlitch 8s infinite;
  animation-delay: 4s;
}

@keyframes glitchOdd {
  0%, 90%, 100% {
    transform: translateX(0) translateY(0);
    color: inherit;
    text-shadow: none;
  }
  10% {
    transform: translateX(-2px) translateY(1px);
    color: #ff0080;
    text-shadow: 2px 0 #00ffff, -2px 0 #ffff00;
  }
  20% {
    transform: translateX(2px) translateY(-1px);
    color: #00ffff;
    text-shadow: -2px 0 #ff0080, 2px 0 #ffff00;
  }
  30% {
    transform: translateX(-1px) translateY(2px);
    color: #ffff00;
    text-shadow: 1px 0 #ff0080, -1px 0 #00ffff;
  }
}

@keyframes glitchEven {
  0%, 85%, 100% {
    transform: translateX(0) translateY(0);
    color: inherit;
    text-shadow: none;
  }
  15% {
    transform: translateX(1px) translateY(-2px);
    color: #00ff80;
    text-shadow: -1px 0 #ff8000, 1px 0 #8000ff;
  }
  30% {
    transform: translateX(-2px) translateY(1px);
    color: #ff8000;
    text-shadow: 2px 0 #00ff80, -2px 0 #8000ff;
  }
  45% {
    transform: translateX(1px) translateY(1px);
    color: #8000ff;
    text-shadow: -1px 0 #ff8000, 1px 0 #00ff80;
  }
}

@keyframes subtleGlitch {
  0%, 96%, 100% {
    transform: translateX(0);
    color: inherit;
    text-shadow: none;
  }
  97% {
    transform: translateX(1px);
    color: #0f0;
    text-shadow: -1px 0 rgba(255, 0, 0, 0.5);
  }
  98% {
    transform: translateX(-1px);
    color: #f0f;
    text-shadow: 1px 0 rgba(0, 255, 255, 0.5);
  }
  99% {
    transform: translateX(0);
    color: #ff0;
    text-shadow: 0 0 3px rgba(255, 255, 0, 0.5);
  }
}

/* Description glitch effects */
.glitch-description {
  position: relative;
}

.glitch-word {
  display: inline-block;
  transition: all 0.2s ease;
}

.glitch-word:nth-child(2n):hover {
  animation: wordGlitch 0.4s ease-in-out;
}

.glitch-word:nth-child(3n) {
  animation: subtleWordGlitch 8s infinite;
  animation-delay: 1s;
}

.glitch-word:nth-child(5n) {
  animation: subtleWordGlitch 12s infinite;
  animation-delay: 6s;
}

@keyframes wordGlitch {
  0%, 80%, 100% {
    transform: translateX(0);
    color: inherit;
  }
  10% {
    transform: translateX(-1px);
    color: #0ff;
  }
  20% {
    transform: translateX(1px);
    color: #f0f;
  }
  30% {
    transform: translateX(-1px);
    color: #ff0;
  }
}

@keyframes subtleWordGlitch {
  0%, 98%, 100% {
    opacity: 1;
    transform: translateX(0);
    color: inherit;
  }
  99% {
    opacity: 0.8;
    transform: translateX(0.5px);
    color: #0f0;
  }
}

.hero-description {
  font-size: 1.3rem;
  line-height: 1.6;
  margin-bottom: 2.5rem;
  color: #ccc;
  max-width: 500px;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.game-container {
  background: #000;
  padding: 1.5rem 1.5rem 1rem 1.5rem; /* Reduced bottom padding */
  color: #fff;
  font-family: 'Space Mono', monospace;
  animation: fadeIn 1.2s ease forwards;
}

.game-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  /* padding: 1rem;  background: linear-gradient(135deg, #001122 0%, #002244 100%); */
  /* border: 1px solid #0f0; */
  border-radius: 4px;
  /* box-shadow: 
    0 0 10px rgba(0, 255, 0, 0.2),
    inset 0 0 10px rgba(0, 255, 0, 0.05); */
}

.game-title {
  font-size: 1.2rem;
  font-weight: 700;
  color: #fff;
  margin: 0;
  letter-spacing: 1px;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.game-controls {
  display: flex;
  gap: 0.5rem;
}

.game-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #fff;
  background: #000;
  color: #fff;
  font-family: 'Space Mono', monospace;
  font-size: 0.8rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s ease;
  text-transform: uppercase;
}

.game-btn:hover {
  background: #fff;
  color: #000;
}

.game-btn.cancel {
  background: #fff;
  color: #000;
}

.game-btn.cancel:hover {
  background: #000;
  color: #fff;
}

.game-stats {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  padding: 0.5rem;
  font-size: 0.8rem;
}

.stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.stat-label {
  font-size: 0.7rem;
  color: #999;
  font-weight: 400;
  margin-bottom: 0.2rem;
}

.stat-value {
  font-weight: 700;
  color: #fff;
  font-size: 0.9rem;
}

.game-board {
  width: 100%;
  height: 350px;
  background: 
    linear-gradient(90deg, #001122 0%, #002244 100%),
    radial-gradient(circle at 20% 20%, #003366 0%, transparent 50%),
    radial-gradient(circle at 80% 80%, #004488 0%, transparent 50%);
  position: relative;
  overflow: hidden;
  outline: none;
  border: 2px solid #fff;
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  image-rendering: crisp-edges;
  transition: all 0.3s ease;
}

.game-board:hover {
  border-color: #fff;
  box-shadow: 
    0 0 30px rgba(255, 255, 255, 0.3),
    inset 0 0 30px rgba(255, 255, 255, 0.1);
}

/* Scanline effect for retro CRT feel */
.game-board::before {
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
  z-index: 1000;
}

/* Pong Game Elements */
.paddle {
  position: absolute;
  z-index: 10;
}

.pixel-paddle {
  width: 10px;
  height: 50px;
  background: #fff;
  border: 1px solid #ccc;
  box-shadow: 0 0 4px rgba(255, 255, 255, 0.6);
}

.ball {
  position: absolute;
  z-index: 10;
}

.pixel-ball {
  width: 8px;
  height: 8px;
  background: #fff;
  border: 1px solid #ccc;
  box-shadow: 0 0 6px rgba(255, 255, 255, 0.8);
  animation: ballGlow 1s ease-in-out infinite alternate;
}

@keyframes ballGlow {
  0% { box-shadow: 0 0 6px rgba(255, 255, 255, 0.8); }
  100% { box-shadow: 0 0 12px rgba(255, 255, 255, 1), 0 0 18px rgba(255, 255, 255, 0.6); }
}

/* Mobile Touch Controls */
.mobile-controls {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 10px;
  z-index: 10;
}

.touch-btn {
  width: 40px;
  height: 40px;
  border: 2px solid #fff;
  background: rgba(0, 0, 0, 0.7);
  color: #fff;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  user-select: none;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  -webkit-tap-highlight-color: transparent;
}

.touch-btn:active {
  background: rgba(255, 255, 255, 0.3);
  transform: scale(0.95);
}

.touch-btn:hover {
  background: rgba(255, 255, 255, 0.2);
}

.center-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 2px;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.line-segment {
  width: 2px;
  height: 15px;
  background: rgba(255, 255, 255, 0.5);
}

.game-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-family: 'Space Mono', monospace;
}

.game-over,
.start-screen,
.pause-screen {
  text-align: center;
  color: #fff;
}

.game-over h4,
.start-screen h4,
.pause-screen h4 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #0f0;
  text-shadow: 0 0 10px #0f0;
  font-family: 'Press Start 2P', 'Space Mono', monospace;
}

.game-over p,
.start-screen p,
.pause-screen p {
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
  color: #fff;
}

.pause-overlay {
  background: rgba(0, 0, 0, 0.7);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .hero {
    padding-top: 80px; /* Add padding to account for fixed navigation */
  }
  
  .hero-content {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    text-align: center;
    padding: 1rem;
  }
  
  .hero-title {
    font-size: 2rem;
    line-height: 1.2;
    margin-bottom: 1rem;
  }
  
  .name {
    font-size: 2.2rem;
    letter-spacing: -1px;
    line-height: 1.1;
  }
  
  .title {
    font-size: 0.9rem;
    letter-spacing: 1px;
    margin-bottom: 1rem;
  }
    .hero-description {
    font-size: 0.9rem;
    max-width: none;
    line-height: 1.5;
    padding: 0 1rem;
  }
  
  .hero-buttons {
    justify-content: center;
    width: 100%;
  }
  
  .game-container {
    margin-top: 1.5rem;
    max-width: 100%;
  }
  
  .game-board {
    height: 250px;
    max-width: 100%;
  }
  
  .game-header {
    flex-direction: column;
    gap: 0.5rem;
    align-items: stretch;
    padding: 0.8rem;
  }
  
  .game-title {
    font-size: 0.8rem;
    margin-bottom: 0.5rem;
  }
  
  .game-controls {
    justify-content: center;
    gap: 0.5rem;
  }
  
  .game-controls span {
    font-size: 0.7rem;
  }
}

@media (max-width: 480px) {
  .hero {
    padding-top: 85px; /* Slightly more padding for smaller screens */
  }
  
  .hero-title {
    font-size: 1.8rem;
  }
  
  .name {
    font-size: 2rem;
  }
  
  .title {
    font-size: 0.8rem;
  }
    .hero-description {
    font-size: 0.85rem;
    padding: 0 0.5rem;
  }
  
  .hero-buttons {
    justify-content: center;
    width: 100%;
  }
  
  .game-container {
    margin-top: 1rem;
  }
  
  .game-board {
    height: 220px;
  }
  
  .game-header {
    padding: 0.6rem;
  }
    .game-title {
    font-size: 0.7rem;
  }
  
  .game-controls span {
    font-size: 0.6rem;
  }
  
  .mobile-controls {
    right: 5px;
  }
  
  .touch-btn {
    width: 35px;
    height: 35px;
    font-size: 16px;
  }
}

/* Particle Effects */
.explosion-particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: #ffffff;
  border-radius: 50%;
  pointer-events: none;
  animation: explode 0.6s ease-out forwards;
}

@keyframes explode {
  0% {
    opacity: 1;
    transform: scale(1);
  }
  100% {
    opacity: 0;
    transform: scale(0) translate(var(--dx, 0), var(--dy, 0));
  }
}

.score-popup {
  position: absolute;
  color: #ffffff;
  font-family: 'Space Mono', monospace;
  font-size: 12px;
  font-weight: bold;
  pointer-events: none;
  animation: scoreFloat 1s ease-out forwards;
  text-shadow: 0 0 4px rgba(255, 255, 255, 0.8);
}

@keyframes scoreFloat {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {    opacity: 0;
    transform: translateY(-30px);
  }
}

.pixel-game-slide {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.pixel-game-slide.animate {
  opacity: 1;
  transform: translateY(0);
}

@keyframes pixelHeroTitle {
  0% { 
    opacity: 0;
    transform: translateY(-20px);
    filter: blur(5px);
  }
  100% { 
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes pixelHeroDesc {
  0% { 
    opacity: 0;
    transform: translateY(20px);
  }
  100% { 
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pixelHeroButtons {
  0% { 
    opacity: 0;
    transform: translateY(30px) scale(0.8);
  }
  100% { 
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes pixelGameGlow {
  0%, 100% { 
    box-shadow: none;
  }
  50% { 
    box-shadow: 
      0 0 30px rgba(255, 255, 255, 0.3),
      inset 0 0 30px rgba(255, 255, 255, 0.1);
  }
}
</style>
