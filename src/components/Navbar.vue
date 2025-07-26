<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isMobileMenuOpen.value = false
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav class="navbar" :class="{ 'scrolled': isScrolled }">
    <div class="nav-container">
      <div class="nav-logo">
        <span class="logo-text">CDP</span>
      </div>
      
      <div class="nav-links" :class="{ 'mobile-open': isMobileMenuOpen }">
        <a @click="scrollToSection('hero')" class="nav-link">Home</a>
        <a @click="scrollToSection('about')" class="nav-link">About</a>
        <a @click="scrollToSection('skills')" class="nav-link">Skills</a>
        <a @click="scrollToSection('experience')" class="nav-link">Experience</a>
        <a @click="scrollToSection('projects')" class="nav-link">Projects</a>
        <a @click="scrollToSection('contact')" class="nav-link">Contact</a>
      </div>
      
      <div class="mobile-toggle" @click="isMobileMenuOpen = !isMobileMenuOpen">
        <span :class="{ 'open': isMobileMenuOpen }"></span>
        <span :class="{ 'open': isMobileMenuOpen }"></span>
        <span :class="{ 'open': isMobileMenuOpen }"></span>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(10, 10, 10, 0.8);
  backdrop-filter: blur(20px);
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(10, 10, 10, 0.95);
  box-shadow: 0 4px 20px rgba(0, 212, 255, 0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-logo {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-links {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.nav-link {
  color: #ffffff;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, #00D4FF, #8B5CF6);
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link:hover {
  color: #00D4FF;
}

.mobile-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
  gap: 4px;
}

.mobile-toggle span {
  width: 25px;
  height: 3px;
  background: #ffffff;
  transition: all 0.3s ease;
}

.mobile-toggle span.open:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.mobile-toggle span.open:nth-child(2) {
  opacity: 0;
}

.mobile-toggle span.open:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -6px);
}

@media (max-width: 768px) {
  .nav-links {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: rgba(10, 10, 10, 0.95);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 2rem;
    transform: translateY(-100vh);
    transition: transform 0.3s ease;
  }

  .nav-links.mobile-open {
    transform: translateY(0);
  }

  .mobile-toggle {
    display: flex;
  }
}
</style>