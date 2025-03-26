<!-- src/layouts/components/CosmicTitle.vue -->
<template>
  <div class="cosmic-title-container">
    <div class="stars-container">
      <div v-for="n in 50" :key="n" class="star"></div>
    </div>
    <div class="cosmic-title">
      <div class="planet-orbit">
        <div class="earth">
          <div class="earth-surface"></div>
          <div class="earth-clouds"></div>
        </div>
      </div>
      <h1 class="title-text">
        <div class="title-main">
          <span class="title-part oshvank">OshVanK</span>
        </div>
        <span class="title-part explorer">Explorer</span>
      </h1>
    </div>
  </div>
</template>

<style scoped>
.cosmic-title-container {
  position: relative;
  width: 100%;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  background-color: #171d30;
  border-radius: 12px;
  margin-bottom: 1.5rem;
  border: 1px solid rgba(100, 116, 139, 0.2);
}

.stars-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.star {
  position: absolute;
  width: 2px;
  height: 2px;
  background-color: white;
  border-radius: 50%;
  animation: twinkle 5s infinite;
}

.star:nth-child(even) {
  width: 3px;
  height: 3px;
}

.star:nth-child(3n) {
  background-color: #4facfe;
}

.star:nth-child(5n) {
  background-color: #00f2fe;
}

/* Her yıldız için farklı konum ve animasyon zamanı */
.star:nth-child(1) { top: 10%; left: 20%; animation-delay: 0.1s; }
.star:nth-child(2) { top: 15%; left: 25%; animation-delay: 0.2s; }
.star:nth-child(3) { top: 20%; left: 30%; animation-delay: 0.3s; }
.star:nth-child(4) { top: 25%; left: 35%; animation-delay: 0.4s; }
.star:nth-child(5) { top: 30%; left: 40%; animation-delay: 0.5s; }
.star:nth-child(6) { top: 35%; left: 45%; animation-delay: 0.6s; }
.star:nth-child(7) { top: 40%; left: 50%; animation-delay: 0.7s; }
.star:nth-child(8) { top: 45%; left: 55%; animation-delay: 0.8s; }
.star:nth-child(9) { top: 50%; left: 60%; animation-delay: 0.9s; }
.star:nth-child(10) { top: 55%; left: 65%; animation-delay: 1s; }
.star:nth-child(11) { top: 60%; left: 70%; animation-delay: 1.1s; }
.star:nth-child(12) { top: 65%; left: 75%; animation-delay: 1.2s; }
.star:nth-child(13) { top: 70%; left: 80%; animation-delay: 1.3s; }
.star:nth-child(14) { top: 75%; left: 85%; animation-delay: 1.4s; }
.star:nth-child(15) { top: 80%; left: 90%; animation-delay: 1.5s; }
.star:nth-child(16) { top: 85%; left: 95%; animation-delay: 1.6s; }
.star:nth-child(17) { top: 90%; left: 10%; animation-delay: 1.7s; }
.star:nth-child(18) { top: 95%; left: 15%; animation-delay: 1.8s; }
.star:nth-child(19) { top: 5%; left: 5%; animation-delay: 1.9s; }
.star:nth-child(20) { top: 10%; left: 95%; animation-delay: 2s; }
.star:nth-child(21) { top: 15%; left: 90%; animation-delay: 2.1s; }
.star:nth-child(22) { top: 20%; left: 85%; animation-delay: 2.2s; }
.star:nth-child(23) { top: 25%; left: 80%; animation-delay: 2.3s; }
.star:nth-child(24) { top: 30%; left: 75%; animation-delay: 2.4s; }
.star:nth-child(25) { top: 35%; left: 70%; animation-delay: 2.5s; }
.star:nth-child(26) { top: 40%; left: 65%; animation-delay: 2.6s; }
.star:nth-child(27) { top: 45%; left: 60%; animation-delay: 2.7s; }
.star:nth-child(28) { top: 50%; left: 55%; animation-delay: 2.8s; }
.star:nth-child(29) { top: 55%; left: 50%; animation-delay: 2.9s; }
.star:nth-child(30) { top: 60%; left: 45%; animation-delay: 3s; }
.star:nth-child(31) { top: 65%; left: 40%; animation-delay: 3.1s; }
.star:nth-child(32) { top: 70%; left: 35%; animation-delay: 3.2s; }
.star:nth-child(33) { top: 75%; left: 30%; animation-delay: 3.3s; }
.star:nth-child(34) { top: 80%; left: 25%; animation-delay: 3.4s; }
.star:nth-child(35) { top: 85%; left: 20%; animation-delay: 3.5s; }
.star:nth-child(36) { top: 90%; left: 15%; animation-delay: 3.6s; }
.star:nth-child(37) { top: 95%; left: 10%; animation-delay: 3.7s; }
.star:nth-child(38) { top: 5%; left: 15%; animation-delay: 3.8s; }
.star:nth-child(39) { top: 10%; left: 20%; animation-delay: 3.9s; }
.star:nth-child(40) { top: 15%; left: 25%; animation-delay: 4s; }
.star:nth-child(41) { top: 20%; left: 30%; animation-delay: 4.1s; }
.star:nth-child(42) { top: 25%; left: 35%; animation-delay: 4.2s; }
.star:nth-child(43) { top: 30%; left: 40%; animation-delay: 4.3s; }
.star:nth-child(44) { top: 35%; left: 45%; animation-delay: 4.4s; }
.star:nth-child(45) { top: 40%; left: 50%; animation-delay: 4.5s; }
.star:nth-child(46) { top: 45%; left: 55%; animation-delay: 4.6s; }
.star:nth-child(47) { top: 50%; left: 60%; animation-delay: 4.7s; }
.star:nth-child(48) { top: 55%; left: 65%; animation-delay: 4.8s; }
.star:nth-child(49) { top: 60%; left: 70%; animation-delay: 4.9s; }
.star:nth-child(50) { top: 65%; left: 75%; animation-delay: 5s; }

@keyframes twinkle {
  0%, 100% {
    opacity: 0.2;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.5);
  }
}

.cosmic-title {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.planet-orbit {
  position: absolute;
  width: 300px;
  height: 300px;
  border: 1px solid rgba(0, 242, 254, 0.2);
  border-radius: 50%;
  animation: rotate 20s linear infinite;
}

.earth {
  position: absolute;
  top: -15px;
  left: 50%;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 242, 254, 0.7), 0 0 20px rgba(0, 242, 254, 0.4);
  transform: translateX(-50%);
}

.earth-surface {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #1e3c72, #2a80b9, #4facfe, #00f2fe);
  animation: rotate-earth 8s linear infinite;
}

.earth-surface::before {
  content: '';
  position: absolute;
  top: 5%;
  left: 10%;
  width: 40%;
  height: 20%;
  background-color: #2ecc71;
  border-radius: 50%;
  transform: rotate(30deg);
}

.earth-surface::after {
  content: '';
  position: absolute;
  bottom: 20%;
  right: 15%;
  width: 30%;
  height: 15%;
  background-color: #2ecc71;
  border-radius: 50%;
  transform: rotate(-20deg);
}

.earth-clouds {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at 30% 30%,
    rgba(255, 255, 255, 0.8) 0%,
    rgba(255, 255, 255, 0) 25%,
    rgba(255, 255, 255, 0.8) 50%,
    rgba(255, 255, 255, 0) 75%
  );
  opacity: 0.5;
  animation: rotate-clouds 5s linear infinite;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate-earth {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate-clouds {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}

.title-text {
  font-size: 4rem;
  font-weight: 800;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  line-height: 1.2;
  position: relative;
}

.title-main {
  display: flex;
  align-items: center;
  justify-content: center;
}

.title-part {
  display: inline-block;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: cosmic-pulse 3s ease-in-out infinite;
}

.oshvank {
  background-image: linear-gradient(135deg, #4facfe, #00f2fe, #0af598);
  font-size: 4.5rem;
}

.explorer {
  display: block;
  width: 100%;
  font-size: 3.5rem;
  margin-top: 0.5rem;
  background-image: linear-gradient(135deg, #4facfe, #00f2fe, #0af598, #4facfe);
  background-size: 300% 100%;
  animation: cosmic-pulse 3s ease-in-out infinite, cosmic-move 6s linear infinite;
}

@keyframes cosmic-pulse {
  0%, 100% {
    filter: drop-shadow(0 0 5px rgba(79, 172, 254, 0.8));
  }
  50% {
    filter: drop-shadow(0 0 15px rgba(79, 172, 254, 0.8));
  }
}

@keyframes cosmic-move {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 300% 50%;
  }
}

/* Meteor animasyonu */
.cosmic-title-container::before {
  content: '';
  position: absolute;
  top: -50px;
  left: -100px;
  width: 3px;
  height: 50px;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0), #4facfe);
  transform: rotate(45deg);
  animation: meteor 6s linear infinite;
  z-index: 2;
}

.cosmic-title-container::after {
  content: '';
  position: absolute;
  top: -30px;
  right: -80px;
  width: 2px;
  height: 30px;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0), #00f2fe);
  transform: rotate(-45deg);
  animation: meteor 8s 3s linear infinite;
  z-index: 2;
}

@keyframes meteor {
  0% {
    transform: translateX(0) translateY(0) rotate(45deg);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  20% {
    transform: translateX(300px) translateY(300px) rotate(45deg);
    opacity: 0;
  }
  100% {
    transform: translateX(300px) translateY(300px) rotate(45deg);
    opacity: 0;
  }
}

/* Responsive düzenlemeler */
@media (max-width: 768px) {
  .cosmic-title-container {
    height: 250px;
  }
  
  .oshvank {
    font-size: 3.5rem;
  }
  
  .explorer {
    font-size: 2.5rem;
  }
  
  .planet-orbit {
    width: 200px;
    height: 200px;
  }
}

@media (max-width: 480px) {
  .cosmic-title-container {
    height: 200px;
  }
  
  .oshvank {
    font-size: 2.5rem;
  }
  
  .explorer {
    font-size: 1.8rem;
  }
  
  .planet-orbit {
    width: 150px;
    height: 150px;
  }
}
</style>
