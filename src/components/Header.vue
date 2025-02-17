<template>
  <header>
    <nav class="navbar">
      <div class="logo">
        <h1><a href="#">Sarvesh Mina</a></h1>
      </div>
      <ul :class="{ 'nav-active': navActive }">
        <li><a href="#summary" @click="smoothScroll($event, 'summary')" :class="{ active: activeSection === 'summary' }">Summary</a></li>
        <li><a href="#education-experience" @click="smoothScroll($event, 'education-experience')" :class="{ active: activeSection === 'education-experience' }">Education & Experience</a></li>
        <li><a href="#skills" @click="smoothScroll($event, 'skills')" :class="{ active: activeSection === 'skills' }">Skills</a></li>
        <li><a href="#projects" @click="smoothScroll($event, 'projects')" :class="{ active: activeSection === 'projects' }">Projects</a></li>
        <li><a href="#contact" @click="smoothScroll($event, 'contact')" :class="{ active: activeSection === 'contact' }">Contact</a></li>
        <li>
          <a href="/assets/SarveshMina.pdf" target="_blank" class="cv-button">📄 View My CV</a>
        </li>
      </ul>
      <!-- Burger Menu for Mobile -->
      <div class="burger" @click="toggleNav" :aria-expanded="navActive" aria-label="Toggle navigation">
        <div :class="{ 'line1': navActive }"></div>
        <div :class="{ 'line2': navActive }"></div>
        <div :class="{ 'line3': navActive }"></div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      navActive: false,
      activeSection: "",
    };
  },
  methods: {
    toggleNav() {
      this.navActive = !this.navActive;
      document.body.classList.toggle("nav-open", this.navActive);
    },
    closeNav() {
      this.navActive = false;
      document.body.classList.remove("nav-open");
    },
    handleScroll() {
      const sections = document.querySelectorAll("section");
      let scrollPosition = window.scrollY + 100;

      sections.forEach((section) => {
        if (
            section.offsetTop <= scrollPosition &&
            section.offsetTop + section.offsetHeight > scrollPosition
        ) {
          this.activeSection = section.getAttribute("id");
        }
      });
    },
    smoothScroll(event, sectionId) {
      event.preventDefault(); // Prevent default jump behavior

      const targetSection = document.getElementById(sectionId);
      if (targetSection) {
        targetSection.scrollIntoView({
          behavior: "smooth",
          block: "start",
        });

        this.closeNav(); // Close mobile nav after clicking
      }
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
};
</script>

<style scoped>
/* Enable Smooth Scrolling for the entire page */
html {
  scroll-behavior: smooth;
}

/* Global Reset */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

header {
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #ffffff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

/* Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

/* Logo */
.logo h1 {
  margin: 0;
  font-size: 1.8rem;
  font-weight: 700;
  font-family: "Source Code Pro", monospace;
}

.logo a {
  text-decoration: none;
  color: #000;
}

/* Navigation Links */
ul {
  list-style: none;
  display: flex;
  gap: 2rem;
}

ul li a {
  color: #333;
  text-decoration: none;
  font-weight: 500;
  font-size: 1rem;
  font-family: "Roboto", sans-serif;
  position: relative;
  transition: color 0.3s ease-in-out;
}

/* Active Section Highlight */
ul li a.active {
  font-weight: bold;
  color: black;
  border-bottom: 2px solid black;
}

/* View My CV Button */
.cv-button {
  background-color: black;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.cv-button:hover {
  background-color: #555;
}

/* Mobile Responsive */
@media (max-width: 768px) {
  ul {
    position: fixed;
    right: 0;
    top: 0;
    height: 100vh;
    background-color: white;
    flex-direction: column;
    align-items: center;
    width: 60%;
    transform: translateX(100%);
    transition: transform 0.5s ease-in-out;
    padding-top: 5rem;
  }

  ul.nav-active {
    transform: translateX(0);
  }

  .burger {
    display: flex;
    flex-direction: column;
  }

  ul li {
    margin: 1.5rem 0;
  }
}
</style>
