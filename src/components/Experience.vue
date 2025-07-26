<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger);

const experiences = [
  {
    title: 'Software Developer',
    company: 'W3Villa Technologies',
    period: '2024 - Present',
    duration: '6+ months',
    description: 'Working as a full-stack developer in a dynamic team environment, contributing to multiple client projects and internal tools. Responsible for both frontend and backend development, database design, and API integration. Gained experience in agile development methodologies and collaborative coding practices.',
    technologies: ['JavaScript', 'TypeScript', 'React.js', 'Node.js', 'Express.js', 'MongoDB', 'MySQL', 'Nest.js'],
    achievements: [
      'Implemented RESTful APIs and database schemas for e-commerce applications',
      'Collaborated with senior developers on code reviews and best practices',
      'Contributed to frontend optimization resulting in improved user experience',
      'Worked with MongoDB and MySQL databases for different project requirements',
      'Gained experience in TypeScript for type-safe development practices'
    ]
  }
]

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '#experience',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  tl.to('#experience', { opacity: 1, visibility: 'visible', duration: 0.5 })
    .from('.timeline-line', {
      height: 0,
      duration: 2,
      ease: 'power2.out',
    }, "-=0.2")
    .from('.timeline-item', {
      x: -100,
      opacity: 0,
      duration: 1,
      stagger: 0.3,
    }, "<0.5"); // "<0.5" starts this 0.5s after the previous animation begins
})
</script>

<template>
  <section id="experience" class="experience-section section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Experience</h2>
        <p class="section-subtitle">My professional journey so far</p>
      </div>
      
      <div class="timeline">
        <div class="timeline-line"></div>
        
        <div 
          v-for="(exp, index) in experiences" 
          :key="index"
          class="timeline-item"
        >
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="experience-card">
              <div class="card-header">
                <div class="title-section">
                  <h3 class="job-title">{{ exp.title }}</h3>
                  <h4 class="company-name">{{ exp.company }}</h4>
                </div>
                <div class="period-section">
                  <span class="period">{{ exp.period }}</span>
                  <span class="duration">{{ exp.duration }}</span>
                </div>
              </div>
              
              <p class="job-description">{{ exp.description }}</p>
              
              <div class="achievements">
                <h5>Key Achievements:</h5>
                <ul class="achievement-list">
                  <li v-for="achievement in exp.achievements" :key="achievement">
                    {{ achievement }}
                  </li>
                </ul>
              </div>
              
              <div class="technologies">
                <h5>Technologies Used:</h5>
                <div class="tech-tags">
                  <span 
                    v-for="tech in exp.technologies" 
                    :key="tech"
                    class="tech-tag"
                  >
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="timeline-item future">
          <div class="timeline-dot future-dot"></div>
          <div class="timeline-content">
            <div class="future-card">
              <h3>What's Next?</h3>
              <p>Always looking for new challenges and opportunities to grow as a developer!</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience-section {
  padding: 100px 2rem;
  background: linear-gradient(135deg, rgba(139, 92, 246, 0.05) 0%, rgba(16, 185, 129, 0.05) 100%);
}

.container {
  max-width: 1000px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  background: linear-gradient(135deg, #8B5CF6, #10B981);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1rem;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #a0a0a0;
}

.timeline {
  position: relative;
  padding: 2rem 0;
}

.timeline-line {
  position: absolute;
  left: 30px;
  top: 0;
  width: 3px;
  height: 100%;
  background: linear-gradient(to bottom, #8B5CF6, #10B981, #00D4FF);
  border-radius: 2px;
}

.timeline-item {
  position: relative;
  margin-bottom: 3rem;
  padding-left: 80px;
}

.timeline-dot {
  position: absolute;
  left: 18px;
  top: 0;
  width: 24px;
  height: 24px;
  background: linear-gradient(135deg, #8B5CF6, #10B981);
  border-radius: 50%;
  border: 4px solid #0a0a0a;
  box-shadow: 0 0 20px rgba(139, 92, 246, 0.5);
}

.future-dot {
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  box-shadow: 0 0 20px rgba(0, 212, 255, 0.5);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.2); opacity: 0.8; }
}

.experience-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  transition: all 0.3s ease;
}

.experience-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(139, 92, 246, 0.1);
  border-color: rgba(139, 92, 246, 0.3);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
  gap: 1rem;
}

.job-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 0.5rem;
}

.company-name {
  font-size: 1.2rem;
  color: #8B5CF6;
  font-weight: 600;
}

.period-section {
  text-align: right;
}

.period {
  display: block;
  font-size: 1rem;
  color: #00D4FF;
  font-weight: 600;
}

.duration {
  display: block;
  font-size: 0.9rem;
  color: #a0a0a0;
  margin-top: 0.25rem;
}

.job-description {
  color: #e0e0e0;
  line-height: 1.7;
  margin-bottom: 1.5rem;
}

.achievements h5,
.technologies h5 {
  color: #10B981;
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.achievement-list {
  list-style: none;
  padding: 0;
  margin-bottom: 1.5rem;
}

.achievement-list li {
  color: #e0e0e0;
  padding: 0.5rem 0;
  position: relative;
  padding-left: 1.5rem;
}

.achievement-list li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: #10B981;
  font-weight: bold;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background: rgba(0, 212, 255, 0.1);
  color: #00D4FF;
  padding: 0.4rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(0, 212, 255, 0.2);
}

.future-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  border: 2px dashed rgba(0, 212, 255, 0.3);
}

.future-card h3 {
  color: #00D4FF;
  font-size: 1.3rem;
  margin-bottom: 1rem;
}

.future-card p {
  color: #a0a0a0;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .timeline-item {
    padding-left: 60px;
  }
  
  .timeline-line {
    left: 20px;
  }
  
  .timeline-dot {
    left: 8px;
  }
  
  .card-header {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .period-section {
    text-align: left;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>
