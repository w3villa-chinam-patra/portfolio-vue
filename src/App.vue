<script setup lang="ts">
// This component now only needs to import the other sections.
// All animation logic will be handled inside each individual component.
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div id="app">
    <Navbar />
    <main>
      <!-- Each section now has the 'section' class and its own ID for scrolling -->
      <Hero id="hero" class="section" />
      <About id="about" class="section" />
      <Skills id="skills" class="section" />
      <Experience id="experience" class="section" />
      <Projects id="projects" class="section" />
      <Contact id="contact" class="section" />
    </main>
    <Footer />
  </div>
</template>

<style>
/* Global styles for your entire application */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  scroll-behavior: smooth;
}
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #0a0a0a;
  color: #ffffff;
  overflow-x: hidden;
}
#app {
  min-height: 100vh;
}

/* This is the key style. It makes all sections invisible by default.
  Each component is now responsible for its own animation to become visible.
*/
.section {
  opacity: 0;
  /* This ensures that even if an animation fails, the element is not interactable */
  visibility: hidden; 
}
</style>
