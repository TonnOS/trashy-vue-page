<template>
  <div class="trash-container">
    <!-- Marquee header because we're TRASHY -->
    <marquee behavior="alternate" scrollamount="15" class="trash-marquee">
      <span v-for="n in 10" :key="n" class="rainbow-text">
        🗑️ WELCOME TO THE TRASH ZONE 🗑️
      </span>
    </marquee>

    <!-- Spinning trash can -->
    <div class="trash-hero">
      <div class="spinning-trash">🗑️</div>
      <h1 class="glitch" data-text="TRASHY VUE PAGE">TRASHY VUE PAGE</h1>
      <p class="trash-subtitle">The internet's garbage collection</p>
    </div>

    <!-- Useless counter -->
    <div class="trash-section">
      <h2>📊 Useless Counter</h2>
      <div class="counter-display">
        <button @click="count--" class="trash-btn">➖</button>
        <span class="count-number">{{ count }}</span>
        <button @click="count++" class="trash-btn">➕</button>
      </div>
      <p class="trash-hint">This counter does absolutely nothing useful.</p>
    </div>

    <!-- Random trash facts -->
    <div class="trash-section">
      <h2>🗑️ Random Trash Facts</h2>
      <div class="fact-box" @click="nextFact">
        <p class="trash-fact">{{ currentFact }}</p>
        <small>Click for more trash knowledge</small>
      </div>
    </div>

    <!-- Ugly color picker -->
    <div class="trash-section">
      <h2>🎨 Make It Uglier</h2>
      <div class="color-buttons">
        <button
          v-for="color in uglyColors"
          :key="color"
          :style="{ backgroundColor: color }"
          @click="backgroundColor = color"
          class="ugly-btn"
        >
          🤮
        </button>
      </div>
    </div>

    <!-- Dancing trash GIFs section -->
    <div class="trash-section">
      <h2>💃 Dancing Trash</h2>
      <div class="dance-floor">
        <span
          v-for="n in 20"
          :key="n"
          class="dancing-emoji"
          :style="{ animationDelay: `${n * 0.1}s` }"
        >
          {{ trashEmojis[n % trashEmojis.length] }}
        </span>
      </div>
    </div>

    <!-- Visitor counter (fake) -->
    <div class="visitor-counter">
      <p>👀 You are visitor number: <strong>{{ fakeVisitorCount }}</strong></p>
      <small>(this number is completely fake)</small>
    </div>

    <!-- Comic Sans footer -->
    <footer class="trash-footer">
      <p>Made with 💩 and Vue.js</p>
      <p class="blink">BEST VIEWED IN INTERNET EXPLORER 6</p>
      <marquee scrollamount="5">
        <span v-for="n in 5" :key="n">
          🚧 UNDER CONSTRUCTION 🚧 | LAST UPDATED: NEVER |
        </span>
      </marquee>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const count = ref(0)
const backgroundColor = ref('#1a1a1a')
const currentFactIndex = ref(0)

const trashFacts = [
  "The average person generates 4.5 pounds of trash per day. You're welcome.",
  "This page is 100% recyclable garbage.",
  "Trash cans were invented in 1875. Before that, people just threw stuff.",
  "The Great Pacific Garbage Patch is 1.6 million square kilometers. This page is smaller.",
  "Recycling one aluminum can saves enough energy to run a TV for 3 hours. This page wastes 3 hours.",
  "Elephants are the only animals that can't jump. This is unrelated to trash.",
  "Bananas are berries. Strawberries are not. Still not trash-related.",
  "The first website is still online. This one shouldn't be.",
  "Your cursor has traveled approximately 0 miles while reading this.",
  "This fact is not a fact. It's trash."
]

const trashEmojis = ['🗑️', '🦝', '🐀', '🦨', '💀', '🤮', '💩', '🪰']

const uglyColors = [
  '#FF00FF', '#00FFFF', '#FF0066', '#66FF00',
  '#FF6600', '#9933FF', '#FF3300', '#00FF00'
]

const currentFact = computed(() => trashFacts[currentFactIndex.value])

const fakeVisitorCount = computed(() => {
  return Math.floor(Math.random() * 999999) + 1
})

function nextFact() {
  currentFactIndex.value = (currentFactIndex.value + 1) % trashFacts.length
}

onMounted(() => {
  // Annoying console message
  console.log('%c🗑️ WELCOME TO THE TRASH ZONE 🗑️',
    'font-size: 30px; color: #FF00FF; background: #000; padding: 20px;')
  console.log('%cWhy are you looking at the console? This page is already garbage.',
    'font-size: 14px; color: #00FFFF;')
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.trash-container {
  min-height: 100vh;
  background-color: v-bind(backgroundColor);
  color: #fff;
  font-family: 'Comic Sans MS', 'Chalkboard SE', 'Comic Neue', cursive;
  overflow-x: hidden;
  transition: background-color 0.5s ease;
}

/* Rainbow text animation */
.rainbow-text {
  background: linear-gradient(90deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  font-size: 1.5rem;
  font-weight: bold;
  margin-right: 2rem;
}

/* Marquee styling */
.trash-marquee {
  background: linear-gradient(90deg, #000, #1a1a1a, #000);
  padding: 10px 0;
  border-bottom: 5px dashed #ff00ff;
}

/* Hero section */
.trash-hero {
  text-align: center;
  padding: 3rem 1rem;
}

.spinning-trash {
  font-size: 8rem;
  animation: spin 2s linear infinite;
  display: inline-block;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Glitch effect */
.glitch {
  font-size: 3rem;
  text-transform: uppercase;
  position: relative;
  color: #fff;
  text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
               0.025em 0.04em 0 #fffc00;
  animation: glitch 725ms infinite;
}

.glitch::before,
.glitch::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.glitch::before {
  left: 2px;
  text-shadow: -2px 0 #ff00c1;
  clip: rect(44px, 450px, 56px, 0);
  animation: glitch-anim 5s infinite linear alternate-reverse;
}

.glitch::after {
  left: -2px;
  text-shadow: -2px 0 #00fff9, 2px 2px #ff00c1;
  animation: glitch-anim2 1s infinite linear alternate-reverse;
}

@keyframes glitch {
  0% { text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff, 0.025em 0.04em 0 #fffc00; }
  15% { text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff, 0.025em 0.04em 0 #fffc00; }
  16% { text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff, -0.05em -0.05em 0 #fffc00; }
  49% { text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff, -0.05em -0.05em 0 #fffc00; }
  50% { text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff, 0 -0.04em 0 #fffc00; }
  99% { text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff, 0 -0.04em 0 #fffc00; }
  100% { text-shadow: -0.05em 0 0 #00fffc, -0.025em -0.04em 0 #fc00ff, -0.04em -0.025em 0 #fffc00; }
}

@keyframes glitch-anim {
  0% { clip: rect(31px, 9999px, 94px, 0); }
  20% { clip: rect(6px, 9999px, 53px, 0); }
  40% { clip: rect(68px, 9999px, 26px, 0); }
  60% { clip: rect(97px, 9999px, 87px, 0); }
  80% { clip: rect(15px, 9999px, 73px, 0); }
  100% { clip: rect(42px, 9999px, 21px, 0); }
}

@keyframes glitch-anim2 {
  0% { clip: rect(65px, 9999px, 100px, 0); }
  20% { clip: rect(12px, 9999px, 45px, 0); }
  40% { clip: rect(89px, 9999px, 67px, 0); }
  60% { clip: rect(34px, 9999px, 12px, 0); }
  80% { clip: rect(78px, 9999px, 91px, 0); }
  100% { clip: rect(23px, 9999px, 56px, 0); }
}

.trash-subtitle {
  font-size: 1.5rem;
  color: #888;
  margin-top: 1rem;
}

/* Sections */
.trash-section {
  background: rgba(255, 255, 255, 0.05);
  border: 3px dashed #ff00ff;
  border-radius: 20px;
  margin: 2rem auto;
  padding: 2rem;
  max-width: 600px;
  text-align: center;
}

.trash-section h2 {
  color: #00ffff;
  text-shadow: 2px 2px #ff00ff;
  margin-bottom: 1.5rem;
}

/* Counter */
.counter-display {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}

.count-number {
  font-size: 4rem;
  color: #ff00ff;
  text-shadow: 3px 3px #00ffff;
  min-width: 100px;
}

.trash-btn {
  font-size: 2rem;
  padding: 1rem 2rem;
  background: linear-gradient(45deg, #ff00ff, #00ffff);
  border: none;
  border-radius: 50%;
  cursor: pointer;
  transition: transform 0.2s;
}

.trash-btn:hover {
  transform: scale(1.2) rotate(10deg);
}

.trash-btn:active {
  transform: scale(0.9);
}

.trash-hint {
  color: #666;
  font-style: italic;
  margin-top: 1rem;
}

/* Fact box */
.fact-box {
  background: linear-gradient(135deg, #2a2a2a, #1a1a1a);
  border: 2px solid #00ffff;
  border-radius: 15px;
  padding: 1.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.fact-box:hover {
  border-color: #ff00ff;
  transform: scale(1.02);
  box-shadow: 0 0 20px rgba(255, 0, 255, 0.5);
}

.trash-fact {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 1rem;
}

/* Color buttons */
.color-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

.ugly-btn {
  font-size: 1.5rem;
  width: 60px;
  height: 60px;
  border-radius: 10px;
  border: 3px solid #fff;
  cursor: pointer;
  transition: all 0.2s;
}

.ugly-btn:hover {
  transform: rotate(180deg) scale(1.2);
}

/* Dance floor */
.dance-floor {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
}

.dancing-emoji {
  font-size: 3rem;
  animation: dance 0.5s ease-in-out infinite alternate;
}

@keyframes dance {
  0% { transform: translateY(0) rotate(0deg); }
  100% { transform: translateY(-20px) rotate(20deg); }
}

/* Visitor counter */
.visitor-counter {
  text-align: center;
  padding: 2rem;
  background: linear-gradient(90deg, #ff00ff33, #00ffff33);
  margin: 2rem auto;
  max-width: 400px;
  border: 2px solid #fff;
  border-radius: 10px;
}

.visitor-counter strong {
  color: #00ff00;
  font-size: 1.5rem;
}

/* Footer */
.trash-footer {
  text-align: center;
  padding: 2rem;
  background: #000;
  border-top: 5px dotted #ff00ff;
  margin-top: 3rem;
}

.trash-footer p {
  margin: 0.5rem 0;
}

.blink {
  animation: blink 1s linear infinite;
  color: #ffff00;
  font-weight: bold;
}

@keyframes blink {
  50% { opacity: 0; }
}

/* Mobile responsiveness */
@media (max-width: 600px) {
  .glitch {
    font-size: 2rem;
  }

  .spinning-trash {
    font-size: 5rem;
  }

  .trash-section {
    margin: 1rem;
    padding: 1rem;
  }

  .counter-display {
    gap: 1rem;
  }

  .count-number {
    font-size: 2.5rem;
  }
}
</style>
