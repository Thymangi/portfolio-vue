<!-- src/components/AppHeader.vue -->
<template>
  <header>
    <div class="logo-container">
      <img
        src="@/assets/logoCarcar.png"
        alt="Logo"
        @click="scrollToTop"
        class="logo"
      />
    </div>
    <nav>
      <ul>
        <li>
          <a href="#presentation" @click="scrollToSection('presentation')"
            >Présentation</a
          >
        </li>
        <li>
          <a href="#creations" @click="scrollToSection('creations')"
            >Créations</a
          >
        </li>
        <li>
          <a href="#contact" @click="scrollToSection('contact')">Contact</a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  methods: {
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      section.scrollIntoView({ behavior: "smooth" });
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: flex-start; /* Aligner les items à droite */
  align-items: center; /* centrer verticalement */
  padding: 1rem;
  background-color: #7d5bf7;
  color: #fff;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1000;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.logo-container {
  display: flex;
  align-items: center;
}

.logo {
  cursor: pointer;
  height: 40px; /* ajuster la taille du logo */
  margin-right: 2rem; /* ajouter de l'espace entre le logo et la nav */
}

nav {
  display: flex;
  align-items: center; /* centre verticalement les éléments de la nav */
}

nav ul {
  display: flex;
  align-items: center; /* Centrer verticalement dans l'ul */
  list-style: none;
  margin: 0;
  padding: 0;
}

nav ul li {
  margin-left: 2rem; /* Ajoutez de l'espace entre les liens */
}

nav ul li a {
  color: #fff;
  text-decoration: none;
  font-size: 1rem; /* ajuster la taille de la font  */
}

nav ul li a:hover,
nav ul li a.active {
  text-decoration: underline;
}
</style>
