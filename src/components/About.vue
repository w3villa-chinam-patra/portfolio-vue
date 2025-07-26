<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '#about',
      start: 'top 80%',
      end: 'bottom 20%',
      toggleActions: 'play none none reverse'
    }
  });

  tl.to('#about', { 
    opacity: 1,
    visibility: 'visible',
    duration: 0.5 
  })
  .from('.about-card, .stat-card', {
    y: 100,
    opacity: 1,
    duration: 0.8,
    stagger: 0.15
  }, "-=0.2");
})
</script>

<template>
  <section id="about" class="about-section section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">About Me</h2>
        <p class="section-subtitle">Get to know more about my journey and passion</p>
      </div>
      
      <div class="about-content">
        <div class="about-text">
          <div class="about-card">
            <h3>My Journey</h3>
            <p>
              My journey into software development began with a fascination for problem-solving and technology. 
              Currently working at W3Villa Technologies for the past 6 months, I've gained valuable experience 
              in full-stack development, working on diverse projects ranging from e-commerce platforms to 
              enterprise applications. I've contributed to both frontend and backend development, learning 
              industry best practices and modern development workflows.
            </p>
          </div>
        </div>
        
        <div class="about-stats">
          <div class="stat-card">
            <div class="stat-number">6+</div>
            <div class="stat-label">Months Experience</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">10+</div>
            <div class="stat-label">Technologies</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">15+</div>
            <div class="stat-label">Projects Worked On</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">100%</div>
            <div class="stat-label">Commitment</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  padding: 100px 2rem;
  background: linear-gradient(135deg, rgba(0, 212, 255, 0.05) 0%, rgba(139, 92, 246, 0.05) 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1rem;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #a0a0a0;
}

.about-content {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 4rem;
  align-items: start;
}

.about-text {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.about-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  transition: all 0.3s ease;
}

.about-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(0, 212, 255, 0.1);
  border-color: rgba(0, 212, 255, 0.3);
}

.about-card h3 {
  font-size: 1.5rem;
  font-weight: 700;
  color: #00D4FF;
  margin-bottom: 1rem;
}

.about-card p {
  line-height: 1.8;
  color: #e0e0e0;
}

.about-stats {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.stat-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem 1rem;
  text-align: center;
  transition: all 0.3s ease;
}

.stat-card:hover {
  transform: scale(1.05);
  border-color: rgba(16, 185, 129, 0.3);
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 800;
  background: linear-gradient(135deg, #10B981, #00D4FF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  color: #a0a0a0;
  font-weight: 500;
}

@media (max-width: 768px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .about-stats {
    grid-template-columns: 1fr 1fr;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>
