<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger);

const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)

const submitForm = async () => {
  isSubmitting.value = true
  
  // Simulate form submission
  await new Promise(resolve => setTimeout(resolve, 2000))
  
  // Reset form
  form.value = {
    name: '',
    email: '',
    subject: '',
    message: ''
  }
  
  isSubmitting.value = false
  alert('Thank you for your message! I\'ll get back to you soon.')
}

const socialLinks = [
  { name: 'LinkedIn', url: 'https://linkedin.com/in/chinam-dibyadyuti-patra', icon: '💼' },
  { name: 'GitHub', url: 'https://github.com/chinam-patra', icon: '🐱' },
  { name: 'Twitter', url: 'https://twitter.com/chinam_patra', icon: '🐦' },
  { name: 'Email', url: 'mailto:chinam.patra@example.com', icon: '📧' }
]

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '#contact',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  tl.to('#contact', { opacity: 1, visibility: 'visible', duration: 0.5 })
    .from('.contact-form', {
      x: -100,
      opacity: 1,
      duration: 1,
    }, "-=0.2")
    .from('.contact-info', {
      x: 100,
      opacity: 1,
      duration: 1,
    }, "<") // "<" starts this at the same time as the previous animation
    .from('.social-link', {
      y: 50,
      opacity: 1,
      duration: 0.8,
      stagger: 0.1,
    }, "-=0.5")
})
</script>

<template>
  <section id="contact" class="contact-section section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Get In Touch</h2>
        <p class="section-subtitle">Ready to work together? Let's create something amazing!</p>
      </div>
      
      <div class="contact-content">
        <div class="contact-form">
          <form @submit.prevent="submitForm">
            <div class="form-group">
              <input 
                v-model="form.name"
                type="text" 
                placeholder="Your Name" 
                required
                class="form-input"
              />
            </div>
            
            <div class="form-group">
              <input 
                v-model="form.email"
                type="email" 
                placeholder="Your Email" 
                required
                class="form-input"
              />
            </div>
            
            <div class="form-group">
              <input 
                v-model="form.subject"
                type="text" 
                placeholder="Subject" 
                required
                class="form-input"
              />
            </div>
            
            <div class="form-group">
              <textarea 
                v-model="form.message"
                placeholder="Your Message" 
                rows="6"
                required
                class="form-input form-textarea"
              ></textarea>
            </div>
            
            <button 
              type="submit" 
              class="submit-btn"
              :disabled="isSubmitting"
              :class="{ 'loading': isSubmitting }"
            >
              <span v-if="!isSubmitting">Send Message</span>
              <span v-else>Sending...</span>
            </button>
          </form>
        </div>
        
        <div class="contact-info">
          <div class="info-card">
            <h3>Let's Connect</h3>
            <p>
              I'm always excited to discuss new opportunities, collaborate on interesting projects, 
              or connect with fellow developers. Whether you're looking for a dedicated full-stack 
              developer, want to discuss a potential project, or just want to chat about technology, 
              I'd love to hear from you! I'm particularly interested in projects involving modern 
              JavaScript frameworks, backend development, and database design.
            </p>
            
            <div class="contact-details">
              <div class="detail-item">
                <span class="detail-icon">📍</span>
                <span class="detail-text">Based in India, Open to Remote Work</span>
              </div>
              <div class="detail-item">
                <span class="detail-icon">💼</span>
                <span class="detail-text">Open to Freelance & Full-time Opportunities</span>
              </div>
              <div class="detail-item">
                <span class="detail-icon">⚡</span>
                <span class="detail-text">Usually responds within 24 hours</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
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

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.contact-form {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-input {
  width: 100%;
  padding: 1rem 1.5rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  color: #ffffff;
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-input::placeholder {
  color: #a0a0a0;
}

.form-input:focus {
  outline: none;
  border-color: #00D4FF;
  box-shadow: 0 0 20px rgba(0, 212, 255, 0.2);
  background: rgba(255, 255, 255, 0.08);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  border: none;
  border-radius: 15px;
  color: white;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 15px 30px rgba(0, 212, 255, 0.3);
}

.submit-btn:disabled {
  opacity: 1;
  cursor: not-allowed;
}

.submit-btn.loading::after {
  content: '';
  position: absolute;
  top: 50%;
  right: 1rem;
  width: 20px;
  height: 20px;
  border: 2px solid transparent;
  border-top: 2px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  transform: translateY(-50%);
}

@keyframes spin {
  0% { transform: translateY(-50%) rotate(0deg); }
  100% { transform: translateY(-50%) rotate(360deg); }
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.info-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
}

.info-card h3 {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
}

.info-card p {
  color: #e0e0e0;
  line-height: 1.7;
  margin-bottom: 2rem;
}

.contact-details {
  margin-bottom: 2rem;
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.detail-icon {
  font-size: 1.2rem;
  min-width: 24px;
}

.detail-text {
  color: #e0e0e0;
  font-weight: 500;
}

.social-links h4 {
  color: #00D4FF;
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.social-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  color: #ffffff;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-link:hover {
  transform: translateY(-3px);
  border-color: rgba(0, 212, 255, 0.3);
  box-shadow: 0 10px 20px rgba(0, 212, 255, 0.1);
}

.social-icon {
  font-size: 1.5rem;
  min-width: 24px;
}

.social-name {
  font-weight: 500;
}

@media (max-width: 768px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .social-grid {
    grid-template-columns: 1fr;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>
