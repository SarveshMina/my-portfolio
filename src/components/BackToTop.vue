<!-- src/components/BackToTop.vue -->
<template>
  <button
      v-if="isVisible"
      class="back-to-top"
      @click="scrollToTop"
      data-aos="fade-in"
      aria-label="Back to Top"
  >
    ↑
  </button>
</template>

<script>
export default {
  name: 'BackToTop',
  data() {
    return {
      isVisible: false
    }
  },
  methods: {
    handleScroll() {
      this.isVisible = window.scrollY > 300
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      })
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style scoped>
.back-to-top {
  position: fixed;
  bottom: 40px;
  right: 40px;
  background-color: var(--button-bg-color);
  color: var(--button-text-color);
  border: none;
  padding: 0.8rem 1rem;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: background-color 0.3s ease, transform 0.3s ease;
  z-index: 1000;
}

.back-to-top:hover {
  background-color: var(--button-hover-bg-color);
  transform: scale(1.1);
}
</style>
