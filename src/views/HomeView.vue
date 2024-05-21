<template>
  <div class="home">
    <section id="presentation" class="presentation">
      <div class="presentation-content">
        <h1>PULLOVER Marc</h1>
        <h2>CARCAR</h2>
        <p>
          CARCAR est spécialisé dans la formation et la prévention du risque
          routier. <br />Nous travaillons auprès des usagers automobiles, deux
          roues, poids lourds et des piétons.
        </p>
        <p></p>
        <div class="usagers">
          <img src="@/assets/auto.png" alt="Automobile" class="usager-image" />
          <img src="@/assets/moto.png" alt="Deux Roues" class="usager-image" />
          <img
            src="@/assets/camion.png"
            alt="Poids Lourd"
            class="usager-image"
          />
          <img src="@/assets/pieton.png" alt="Piéton" class="usager-image" />
        </div>
        <div class="complement">
          <p>
            Nos Services Formation des Conducteurs : Nous proposons des
            programmes de formation personnalisés pour les automobilistes,
            motocyclistes, conducteurs de poids lourds et piétons. Nos
            formations visent à améliorer les compétences des conducteurs et à
            promouvoir une conduite responsable. Consultation en Sécurité
            Routière : Nos experts offrent des services de consultation pour
            aider les entreprises à mettre en place des politiques de sécurité
            routière efficaces. Nous travaillons en étroite collaboration avec
            nos clients pour identifier les risques et développer des stratégies
            de prévention. Audit de Sécurité : Nous réalisons des audits
            complets de sécurité routière pour identifier les dangers potentiels
            et fournir des recommandations pour améliorer la sécurité sur les
            routes. Nos audits sont basés sur des analyses rigoureuses et des
            normes de sécurité reconnues. Pourquoi choisir RoadSafe ? Expertise
            : Notre équipe est composée de professionnels expérimentés et
            passionnés par la sécurité routière. Nous utilisons les dernières
            technologies et méthodologies pour offrir des services de qualité
            supérieure. Personnalisation : Chaque client est unique. Nous
            adaptons nos services pour répondre aux besoins spécifiques de
            chaque usager, qu'il soit particulier ou professionnel. Engagement :
            La sécurité routière est notre priorité. Nous nous engageons à
            fournir des solutions pratiques et efficaces pour réduire les
            risques et promouvoir une conduite sécurisée. Rejoignez-nous dans
            notre mission pour rendre les routes plus sûres pour tous. Pour plus
            d'informations sur nos services et pour découvrir comment nous
            pouvons vous aider, n'hésitez pas à nous contacter.
          </p>
        </div>
      </div>
    </section>
    <section id="creations">
      <h2>Mes Créations</h2>
      <div class="creations">
        <div class="creation" v-for="creation in creations" :key="creation.id">
          <img
            :src="creation.image"
            :alt="creation.title"
            class="creation-image"
            @click="openModal(creation)"
          />
          <h3>{{ creation.title }}</h3>
        </div>
      </div>
      <CreationModal
        :visible="modalVisible"
        :creation="selectedCreation"
        @close="closeModal"
      />
    </section>
    <section id="contact">
      <h2>Contactez-moi</h2>
      <ContactForm />
    </section>
    <button @click="scrollToTop" class="back-to-top" v-if="showButton">
      &#9650;
    </button>
  </div>
</template>

<script>
import CreationModal from "../components/CreationModal.vue";
import ContactForm from "../components/ContactForm.vue";

export default {
  components: {
    CreationModal,
    ContactForm,
  },
  data() {
    return {
      creations: [
        {
          id: 1,
          image: require("../assets/cv_cef.png"),
          title: "CV html-css",
          date: "2022-01-01",
          technologies: "VueJS, HTML5, CSS3",
          link: "https://example.com/creation1",
          repo: "https://github.com/your-profile/creation1",
        },
        {
          id: 2,
          image: require("../assets/cv_cef2.png"),
          title: "Création 2",
          date: "2023-01-01",
          technologies: "React, JavaScript",
          link: "https://example.com/creation2",
          repo: "https://github.com/your-profile/creation2",
        },
        {
          id: 3,
          image: require("../assets/cv_cef3.png"),
          title: "Création 3",
          date: "2024-01-01",
          technologies: "Angular, TypeScript",
          link: "https://example.com/creation3",
          repo: "https://github.com/your-profile/creation3",
        },
      ],
      modalVisible: false,
      selectedCreation: null,
      showButton: false,
    };
  },
  methods: {
    openModal(creation) {
      this.selectedCreation = creation;
      this.modalVisible = true;
    },
    closeModal() {
      this.modalVisible = false;
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
    checkScroll() {
      this.showButton = window.scrollY > 200;
    },
  },
  created() {
    window.addEventListener("scroll", this.checkScroll);
  },
  destroyed() {
    window.removeEventListener("scroll", this.checkScroll);
  },
};
</script>

<style scoped>
.home {
  background: linear-gradient(
    to bottom,
    #001f3f,
    #800080
  ); /* Dégradé de bleu nuit à violet */
  color: white; /* Couleur du texte en blanc */
  padding-top: 60px; /* Pour compenser le header fixe */
  padding-bottom: 80px; /* Pour éviter que le contenu soit caché derrière le footer */
  position: relative;
}

section {
  padding: 5rem 2rem 2rem;
}
.presentation {
  display: flex;
  flex-direction: column;
  align-items: center; /* Center content horizontally */
  justify-content: center; /* Center content vertically */
  text-align: center; /* Center text */
  margin-top: 2rem; /* Add some margin on top */
  min-height: 100vh; /* Ensure the section takes at least the full height of the viewport */
}
.presentation-content {
  margin-top: 1rem; /* Reduce the margin at the top */
  margin-bottom: auto; /* Center the content vertically */
  max-width: 800px; /* Optionally limit the width of the content */
}

.usagers {
  display: flex;
  justify-content: center;
  flex-direction: row;
  gap: 2rem; /* Space between images */
  margin-top: 2rem; /* Add some margin on top */
}

.usager-image {
  width: 100px; /* Adjust the size of the images */
  height: auto;
}
.complement {
  display: flex;
  justify-content: center;
  margin-top: 2rem; /* Add some margin on top */
  text-align: center; /* Center text */
}
.creations {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.creation {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.creation-image {
  width: 80%;
  max-width: 500px;
  height: auto;
  transition: box-shadow 0.3s;
}

.creation-image:hover {
  box-shadow: 0 8px 16px rgba(241, 225, 225, 0.4);
  cursor: pointer; /* Change cursor on hover */
}

.creation h3 {
  text-align: center;
  margin-top: 1rem;
  font-size: 2vw;
}

@media (max-width: 768px) {
  .creation-image {
    width: 90%;
  }

  .creation h3 {
    font-size: 4vw;
  }
}

@media (max-width: 480px) {
  .creation-image {
    width: 100%;
  }

  .creation h3 {
    font-size: 5vw;
  }
}

.back-to-top {
  position: fixed;
  bottom: 80px; /* Adjusted to be above the footer */
  right: 20px;
  padding: 10px 20px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, opacity 0.3s;
  font-size: 24px;
  line-height: 1;
}

.back-to-top:hover {
  background-color: #555;
}

.back-to-top:after {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: white;
  box-shadow: 0 0 15px white;
  position: absolute;
  top: -10px;
  right: -10px;
}
</style>
