<script setup lang="ts">
import { ref } from 'vue'

const currentYear = ref(new Date().getFullYear())

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-top">
        <div class="footer-logo">
          <h3>Chinam Dibyadyuti Patra</h3>
          <p>Software Developer</p>
        </div>
        
        <div class="footer-links">
          <div class="link-group">
            <h4>Navigation</h4>
            <ul>
              <li><a href="#hero">Home</a></li>
              <li><a href="#about">About</a></li>
              <li><a href="#skills">Skills</a></li>
              <li><a href="#experience">Experience</a></li>
            </ul>
          </div>
          
          <div class="link-group">
            <h4>Projects</h4>
            <ul>
              <li><a href="#projects">Featured Work</a></li>
              <li><a href="#contact">Get In Touch</a></li>
            </ul>
          </div>
        </div>
        
        <button @click="scrollToTop" class="back-to-top">
          <span>↑</span>
        </button>
      </div>
      
      <div class="footer-bottom">
        <div class="footer-divider"></div>
        <div class="footer-info">
          <p>&copy; {{ currentYear }} Chinam Dibyadyuti Patra. All rights reserved.</p>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 100%);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 3rem 2rem 2rem;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
}

.footer-top {
  display: grid;
  grid-template-columns: 1fr 2fr auto;
  gap: 3rem;
  align-items: start;
  margin-bottom: 2rem;
}

.footer-logo h3 {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.footer-logo p {
  color: #a0a0a0;
  font-weight: 500;
}

.footer-links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.link-group h4 {
  color: #ffffff;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.link-group ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.link-group li {
  margin-bottom: 0.5rem;
}

.link-group a {
  color: #a0a0a0;
  text-decoration: none;
  transition: color 0.3s ease;
  font-size: 0.9rem;
}

.link-group a:hover {
  color: #00D4FF;
}

.back-to-top {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  border: none;
  border-radius: 50%;
  color: white;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.back-to-top:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 212, 255, 0.3);
}

.footer-divider {
  width: 100%;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  margin-bottom: 1.5rem;
}

.footer-info {
  text-align: center;
}

.footer-info p {
  color: #a0a0a0;
  margin-bottom: 0.5rem;
}

.footer-subtitle {
  font-size: 0.9rem;
  color: #666;
}

@media (max-width: 768px) {
  .footer-top {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }
  
  .footer-links {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .back-to-top {
    justify-self: center;
  }
}
</style>