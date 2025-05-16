<template>
  <div class="container" @click="openCard">
    <!-- Animated Background Elements -->
    <div class="sparkles">
      <div v-for="(sparkle, index) in sparkles" 
           :key="index" 
           class="sparkle" 
           :style="sparkle.style"></div>
    </div>

    <!-- Main Card -->
    <div class="card" :class="{ opened: isOpened }">
      <div class="heart-container">
        <div class="pulse-heart">💖</div>
        <div class="heart-flap"></div>
      </div>
      
      <!-- Message Content -->
      <transition name="message">
        <div v-if="isOpened" class="message-content">
          <h1 class="name">Elissa</h1>
          <div class="message">
            <p class="line">Every moment without you</p>
            <p class="line">feels like a paused melody...</p>
            <p class="main-text">I Miss You</p>
          </div>
          <div class="floating-hearts">
            <span v-for="n in 3" :key="n" class="floating-heart">💖</span>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpened: false,
      sparkles: Array(20).fill().map(() => ({
        style: {
          left: Math.random() * 100 + '%',
          top: Math.random() * 100 + '%',
          animationDelay: Math.random() * 2 + 's'
        }
      }))
    }
  },
  methods: {
    openCard() {
      if (!this.isOpened) {
        this.isOpened = true;
        this.addHearts();
      }
    },
    addHearts() {
      // Add bursting hearts animation
      for (let i = 0; i < 5; i++) {
        this.sparkles.push({
          style: {
            left: Math.random() * 100 + '%',
            top: Math.random() * 100 + '%',
            animationDelay: Math.random() + 's'
          }
        });
      }
    }
  }
}
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #ffafbd, #ffc3a0);
  cursor: pointer;
  overflow: hidden;
  position: relative;
}

.card {
  position: relative;
  width: 320px;
  height: 400px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  transition: transform 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
  transform-style: preserve-3d;
  perspective: 1000px;
}

.card.opened {
  transform: rotateY(180deg) scale(1.05);
}

.heart-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.4s ease;
}

.pulse-heart {
  font-size: 4rem;
  animation: pulse 1.5s ease-in-out infinite;
  text-shadow: 0 0 15px rgba(255, 65, 108, 0.5);
}

.heart-flap {
  position: absolute;
  width: 100px;
  height: 100px;
  background: white;
  clip-path: polygon(0 0, 100% 0, 50% 50%);
  opacity: 0;
  transition: all 0.4s ease;
}

.message-content {
  position: absolute;
  width: 100%;
  height: 100%;
  padding: 2rem;
  backface-visibility: hidden;
  transform: rotateY(180deg);
}

.name {
  font-family: 'Great Vibes', cursive;
  color: #ff416c;
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 1.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.message {
  text-align: center;
  color: #555;
  line-height: 1.6;
}

.main-text {
  font-size: 2rem;
  color: #ff416c;
  margin: 1.5rem 0;
  font-weight: bold;
  animation: textGlow 2s ease-in-out infinite;
}

.floating-hearts {
  position: absolute;
  bottom: 20px;
  width: 100%;
  text-align: center;
}

.floating-heart {
  font-size: 1.5rem;
  margin: 0 8px;
  display: inline-block;
  animation: float 3s ease-in-out infinite;
}

.sparkle {
  position: absolute;
  width: 8px;
  height: 8px;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  animation: sparkle 1.5s infinite;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.2); }
  100% { transform: scale(1); }
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

@keyframes textGlow {
  0%, 100% { text-shadow: 0 0 10px rgba(255, 65, 108, 0.3); }
  50% { text-shadow: 0 0 20px rgba(255, 65, 108, 0.6); }
}

@keyframes sparkle {
  0% { transform: scale(0); opacity: 1; }
  100% { transform: scale(3); opacity: 0; }
}

.message-enter-active {
  transition: all 0.5s ease 0.3s;
}

.message-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

@media (max-width: 480px) {
  .card {
    width: 90%;
    height: 80vh;
  }
}
</style>