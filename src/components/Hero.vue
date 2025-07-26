<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const typewriterText = ref('')
const roles = ['Software Developer', 'Full Stack Engineer', 'Backend Specialist', 'Tech Enthusiast']
let currentRoleIndex = 0

const typeWriter = () => {
  const currentRole = roles[currentRoleIndex]
  let charIndex = 0
  
  const type = () => {
    if (charIndex < currentRole.length) {
      typewriterText.value += currentRole.charAt(charIndex)
      charIndex++
      setTimeout(type, 100)
    } else {
      setTimeout(() => {
        const erase = () => {
          if (typewriterText.value.length > 0) {
            typewriterText.value = typewriterText.value.slice(0, -1)
            setTimeout(erase, 50)
          } else {
            currentRoleIndex = (currentRoleIndex + 1) % roles.length
            setTimeout(typeWriter, 500)
          }
        }
        setTimeout(erase, 2000)
      }, 1000)
    }
  }
  type()
}

onMounted(() => {
  const tl = gsap.timeline();

  // 1. First, make the entire Hero section visible. This is the crucial fix.
  tl.to('#hero', { opacity: 1, visibility: 'visible', duration: 0.5 })
  
    // 2. Then, animate the rest of the elements.
    .from('.hero-name', { y: 100, opacity: 0, duration: 1, ease: 'power3.out' }, "-=0.2")
    .from('.hero-subtitle', { y: 50, opacity: 0, duration: 0.8, ease: 'power3.out' }, '-=0.5')
    .from('.hero-description', { y: 30, opacity: 0, duration: 0.8, ease: 'power3.out' }, '-=0.3')
    .from('.hero-buttons', { y: 30, opacity: 0, duration: 0.8, ease: 'power3.out' }, '-=0.3')
    .from('.floating-elements', { scale: 0, opacity: 0, duration: 1, stagger: 0.2, ease: 'back.out(1.7)' }, '-=0.5')

  setTimeout(typeWriter, 1500)

  gsap.to('.floating-1', {
    y: -20,
    duration: 3,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut'
  })

  gsap.to('.floating-2', {
    y: -30,
    duration: 4,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut',
    delay: 1
  })

  gsap.to('.floating-3', {
    y: -25,
    duration: 3.5,
    repeat: -1,
    yoyo: true,
    ease: 'power2.inOut',
    delay: 2
  })
})

const scrollToContact = () => {
  document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
}

</script>

<template>
  <section id="hero" class="hero section">
    <div class="hero-background">
      <div class="gradient-orb orb-1"></div>
      <div class="gradient-orb orb-2"></div>
      <div class="gradient-orb orb-3"></div>
    </div>
    
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-name">
          Hi, I'm <span class="name-highlight">Chinam Dibyadyuti Patra</span>
        </h1>
        <div class="hero-subtitle">
          <span class="typewriter">{{ typewriterText }}</span>
          <span class="cursor">|</span>
        </div>
        <p class="hero-description">
          Passionate full-stack developer with 6 months of hands-on experience at W3Villa Technologies. 
          I specialize in building scalable web applications using modern JavaScript frameworks, 
          backend technologies, and databases. I love turning complex problems into elegant solutions 
          and am always eager to learn new technologies and best practices.
        </p>
        <div class="hero-buttons">
          <button @click="scrollToContact" class="btn-primary">Get In Touch</button>
        </div>
      </div>
      
      <div class="hero-visual">
        <div class="floating-elements floating-1">
          <div class="code-block">
            <span class="code-line">const developer = {</span>
            <span class="code-line">  name: 'Chinam',</span>
            <span class="code-line">  passion: 'coding'</span>
            <span class="code-line">};</span>
          </div>
        </div>
        <div class="floating-elements floating-2">
          <div class="tech-icon">💻</div>
        </div>
        <div class="floating-elements floating-3">
          <div class="tech-icon">🚀</div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding: 0 2rem;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
}

.gradient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.3;
}

.orb-1 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  top: 10%;
  right: 10%;
  animation: float 6s ease-in-out infinite;
}

.orb-2 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #10B981, #00D4FF);
  bottom: 20%;
  left: 10%;
  animation: float 8s ease-in-out infinite reverse;
}

.orb-3 {
  width: 200px;
  height: 200px;
  background: linear-gradient(135deg, #8B5CF6, #10B981);
  top: 50%;
  left: 50%;
  animation: float 7s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-30px); }
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-name {
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.name-highlight {
  background: linear-gradient(135deg, #00D4FF, #8B5CF6, #10B981);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
  color: #00D4FF;
  min-height: 2.5rem;
}

.cursor {
  animation: blink 1s infinite;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

.hero-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #a0a0a0;
  margin-bottom: 2rem;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn-primary, .btn-secondary {
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-primary {
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  color: white;
  box-shadow: 0 10px 30px rgba(0, 212, 255, 0.3);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(0, 212, 255, 0.4);
}

.btn-secondary {
  background: transparent;
  color: #00D4FF;
  border: 2px solid #00D4FF;
}

.btn-secondary:hover {
  background: #00D4FF;
  color: #0a0a0a;
  transform: translateY(-3px);
}

.hero-visual {
  position: relative;
  height: 500px;
}

.floating-elements {
  position: absolute;
}

.floating-1 {
  top: 20%;
  right: 10%;
}

.floating-2 {
  top: 60%;
  right: 60%;
}

.floating-3 {
  top: 10%;
  right: 70%;
}

.code-block {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 1.5rem;
  font-family: 'Monaco', monospace;
  font-size: 0.9rem;
  line-height: 1.5;
}

.code-line {
  display: block;
  color: #00D4FF;
}

.tech-icon {
  font-size: 3rem;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }
  
  .hero-name {
    font-size: 2.5rem;
  }
  
  .hero-subtitle {
    font-size: 1.4rem;
  }
  
  .hero-visual {
    height: 300px;
  }
  
  .floating-elements {
    scale: 0.8;
  }
}
</style>
