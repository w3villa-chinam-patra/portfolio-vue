<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger);

const skills = [
  { name: 'HTML5', level: 90, category: 'Frontend', icon: '🔖' },
  { name: 'CSS3', level: 88, category: 'Frontend', icon: '🎨' },
  { name: 'JavaScript', level: 85, category: 'Frontend', icon: '⚡' },
  { name: 'TypeScript', level: 78, category: 'Frontend', icon: '📘' },
  { name: 'React.js', level: 80, category: 'Frontend', icon: '⚛️' },
  { name: 'Node.js', level: 82, category: 'Backend', icon: '🟢' },
  { name: 'Express.js', level: 85, category: 'Backend', icon: '🚂' },
  { name: 'Nest.js', level: 75, category: 'Backend', icon: '🐱' },
  { name: 'Sails.js', level: 70, category: 'Backend', icon: '⛵' },
  { name: 'Spring Boot', level: 78, category: 'Backend', icon: '🍃' },
  { name: 'MongoDB', level: 80, category: 'Database', icon: '🍃' },
  { name: 'MySQL', level: 83, category: 'Database', icon: '🐬' }
]

const categories = ['All', 'Frontend', 'Backend', 'Database']
const selectedCategory = ref('All')

const filteredSkills = ref(skills)

const filterSkills = (category: string) => {
  selectedCategory.value = category
  if (category === 'All') {
    filteredSkills.value = skills
  } else {
    filteredSkills.value = skills.filter(skill => skill.category === category)
  }
  
  // Re-animate filtered skills
  gsap.from('.skill-card', {
    scale: 1,
    opacity: 1,
    duration: 0.5,
    stagger: 0.1,
    ease: 'back.out(1.7)'
  })
}

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '#skills',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  tl.to('#skills', { opacity: 1, visibility: 'visible', duration: 0.5 })
    .from('.skill-card', {
      scale: 1,
      opacity: 1,
      duration: 0.8,
      stagger: 0.1,
      ease: 'back.out(1.7)',
    }, "-=0.2")
    .from('.progress-fill', {
      width: 0,
      duration: 1.5,
      ease: 'power2.out',
      stagger: 0.1,
    }, "<"); // "<" starts this animation at the same time as the previous one
})
</script>

<template>
  <section id="skills" class="skills-section section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Skills & Technologies</h2>
        <p class="section-subtitle">Technologies I work with and love</p>
      </div>
      
      <div class="filter-tabs">
        <button 
          v-for="category in categories" 
          :key="category"
          @click="filterSkills(category)"
          class="filter-tab"
          :class="{ active: selectedCategory === category }"
        >
          {{ category }}
        </button>
      </div>
      
      <div class="skills-grid">
        <div 
          v-for="skill in filteredSkills" 
          :key="skill.name"
          class="skill-card"
        >
          <div class="skill-icon">{{ skill.icon }}</div>
          <div class="skill-info">
            <h3 class="skill-name">{{ skill.name }}</h3>
            <div class="skill-category">{{ skill.category }}</div>
            <div class="progress-bar">
              <div 
                class="progress-fill" 
                :style="{ width: skill.level + '%' }"
              ></div>
            </div>
            <div class="skill-level">{{ skill.level }}%</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  padding: 100px 2rem;
  background: #0a0a0a;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
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

.filter-tabs {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-tab {
  padding: 0.8rem 1.5rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 25px;
  color: #a0a0a0;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
}

.filter-tab:hover {
  border-color: rgba(0, 212, 255, 0.3);
  color: #00D4FF;
}

.filter-tab.active {
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  color: white;
  border-color: transparent;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.skill-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(0, 212, 255, 0.1);
  border-color: rgba(0, 212, 255, 0.3);
}

.skill-icon {
  font-size: 2.5rem;
  min-width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 15px;
}

.skill-info {
  flex: 1;
}

.skill-name {
  font-size: 1.3rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 0.5rem;
}

.skill-category {
  font-size: 0.9rem;
  color: #00D4FF;
  margin-bottom: 1rem;
  font-weight: 500;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
  margin-bottom: 0.5rem;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(135deg, #00D4FF, #10B981);
  border-radius: 3px;
  transition: width 1.5s ease;
}

.skill-level {
  font-size: 0.9rem;
  color: #a0a0a0;
  font-weight: 600;
}

@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
  
  .skill-card {
    flex-direction: column;
    text-align: center;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>
