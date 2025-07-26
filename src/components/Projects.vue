<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger);

const projects = [
  {
    title: 'E-Commerce Web Application',
    description: 'A comprehensive e-commerce platform built during my time at W3Villa Technologies. Features include user authentication, product catalog, shopping cart, order management, and admin dashboard.',
    image: 'https://images.pexels.com/photos/230544/pexels-photo-230544.jpeg?auto=compress&cs=tinysrgb&w=600',
    technologies: ['React.js', 'Node.js', 'Express.js', 'MongoDB', 'JWT Authentication'],
    features: ['User Registration & Login', 'Product Catalog with Search', 'Shopping Cart & Checkout', 'Order History', 'Admin Panel for Product Management', 'Responsive Design'],
    github: '#',
    demo: '#',
    status: 'Completed'
  },
  {
    title: 'Restaurant Management System',
    description: 'A full-stack restaurant management application with menu management, order processing, and customer management. Built using modern web technologies with a focus on user experience.',
    image: 'https://images.pexels.com/photos/3184306/pexels-photo-3184306.jpeg?auto=compress&cs=tinysrgb&w=600',
    technologies: ['React.js', 'Nest.js', 'TypeScript', 'MySQL', 'JWT'],
    features: ['Menu Management', 'Order Processing', 'Customer Database', 'Sales Analytics', 'Staff Management', 'Responsive Interface'],
    github: '#',
    demo: '#',
    status: 'Completed'
  },
  {
    title: 'Personal Finance Tracker',
    description: 'A web application for tracking personal expenses and income with data visualization. Features budget planning, expense categorization, and financial insights with interactive charts.',
    image: 'https://images.pexels.com/photos/164527/pexels-photo-164527.jpeg?auto=compress&cs=tinysrgb&w=600',
    technologies: ['HTML5', 'CSS3', 'JavaScript', 'Chart.js', 'Local Storage'],
    features: ['Expense Tracking', 'Income Management', 'Budget Planning', 'Data Visualization', 'Category-wise Analysis', 'Export Reports'],
    github: '#',
    demo: '#',
    status: 'Completed'
  },
]

const selectedProject = ref(null)


onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '#projects',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  tl.to('#projects', { opacity: 1, visibility: 'visible', duration: 0.5 })
    .from('.project-card', {
      y: 100,
      opacity: 1,
      duration: 0.8,
      stagger: 0.2,
    }, "-=0.2");
})
</script>

<template>
  <section id="projects" class="projects-section section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Featured Projects</h2>
        <p class="section-subtitle">Some of my recent work and side projects</p>
      </div>
      
      <div class="projects-grid">
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          class="project-card"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
            <div class="project-overlay">
              <div class="project-status" :class="project.status.toLowerCase().replace(' ', '-')">
                {{ project.status }}
              </div>
            </div>
          </div>
          
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-tech">
              <span 
                v-for="tech in project.technologies.slice(0, 3)" 
                :key="tech"
                class="tech-tag"
              >
                {{ tech }}
              </span>
              <span v-if="project.technologies.length > 3" class="more-tech">
                +{{ project.technologies.length - 3 }} more
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Project Modal -->
    <div v-if="selectedProject" class="project-modal">
      <div class="modal-content" @click.stop>
        <button class="close-btn">&times;</button>
        
        <div class="modal-header">
          <img :src="selectedProject.image" :alt="selectedProject.title" />
          <div class="modal-title-section">
            <h2>{{ selectedProject.title }}</h2>
            <div class="project-status" :class="selectedProject.status.toLowerCase().replace(' ', '-')">
              {{ selectedProject.status }}
            </div>
          </div>
        </div>
        
        <div class="modal-body">
          <p class="modal-description">{{ selectedProject.description }}</p>
          
          <div class="modal-section">
            <h4>Key Features</h4>
            <ul class="features-list">
              <li v-for="feature in selectedProject.features" :key="feature">
                {{ feature }}
              </li>
            </ul>
          </div>
          
          <div class="modal-section">
            <h4>Technologies Used</h4>
            <div class="modal-tech-tags">
              <span 
                v-for="tech in selectedProject.technologies" 
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
  </section>
</template>

<style scoped>
.projects-section {
  padding: 100px 2rem;
  background: #0a0a0a;
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

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 30px 60px rgba(0, 212, 255, 0.15);
  border-color: rgba(0, 212, 255, 0.3);
}

.project-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 1rem;
  right: 1rem;
}

.project-status {
  padding: 0.4rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
}

.project-status.completed {
  background: rgba(16, 185, 129, 0.2);
  color: #10B981;
  border: 1px solid rgba(16, 185, 129, 0.3);
}

.project-status.in-progress {
  background: rgba(0, 212, 255, 0.2);
  color: #00D4FF;
  border: 1px solid rgba(0, 212, 255, 0.3);
}

.project-content {
  padding: 2rem;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
}

.project-description {
  color: #a0a0a0;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  background: rgba(0, 212, 255, 0.1);
  color: #00D4FF;
  padding: 0.3rem 0.6rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(0, 212, 255, 0.2);
}

.more-tech {
  color: #8B5CF6;
  font-size: 0.8rem;
  font-weight: 500;
}

.project-actions {
  display: flex;
  gap: 1rem;
}

.action-btn {
  flex: 1;
  padding: 0.8rem 1rem;
  border-radius: 12px;
  text-decoration: none;
  text-align: center;
  font-weight: 600;
  font-size: 0.9rem;
  transition: all 0.3s ease;
  border: 1px solid transparent;
}

.action-btn.github {
  background: rgba(255, 255, 255, 0.05);
  color: #ffffff;
  border-color: rgba(255, 255, 255, 0.1);
}

.action-btn.github:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.3);
}

.action-btn.demo {
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  color: white;
}

.action-btn.demo:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(0, 212, 255, 0.3);
}

/* Modal Styles */
.project-modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 2rem;
}

.modal-content {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  max-width: 800px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  color: #ffffff;
  font-size: 2rem;
  cursor: pointer;
  z-index: 1001;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.close-btn:hover {
  background: rgba(255, 0, 0, 0.2);
}

.modal-header {
  position: relative;
  height: 300px;
  overflow: hidden;
  border-radius: 20px 20px 0 0;
}

.modal-header img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-title-section {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  padding: 3rem 2rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}

.modal-title-section h2 {
  font-size: 2rem;
  font-weight: 700;
  color: #ffffff;
  margin: 0;
}

.modal-body {
  padding: 2rem;
}

.modal-description {
  font-size: 1.1rem;
  color: #e0e0e0;
  line-height: 1.7;
  margin-bottom: 2rem;
}

.modal-section {
  margin-bottom: 2rem;
}

.modal-section h4 {
  color: #00D4FF;
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.features-list {
  list-style: none;
  padding: 0;
}

.features-list li {
  color: #e0e0e0;
  padding: 0.5rem 0;
  position: relative;
  padding-left: 1.5rem;
}

.features-list li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: #10B981;
  font-weight: bold;
}

.modal-tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
}

.modal-actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .project-modal {
    padding: 1rem;
  }
  
  .modal-title-section {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }
  
  .modal-actions {
    flex-direction: column;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>
