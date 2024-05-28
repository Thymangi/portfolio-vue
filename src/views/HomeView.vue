<template>
  <div class="home">
    <section id="presentation" class="presentation">
      <div class="presentation-content">
        <h1>PULLOVER Marc</h1>
        <h2>CARCAR</h2>
        <p>
          CARCAR est spécialisé dans la formation et la prévention du risque
          routier. <br />Nous travaillons auprès des différents usagers: les
          automobilistes, les conducteurs de deux roues, de poids lourds et les
          piétons.
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
      <!-- Création 1 et 3 avec lien gitHub -->
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
      <div class="creation">
        <!-- Création 2 avec lien pdf -->
        <a href="creation.link" target="_blank"> </a>
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
          repo: "https://github.com/Thymangi/cef_cv_2024",
          images: [
            require("@/assets/cv_cef.png"),
            require("@/assets/cv_cef2.png"),
            require("@/assets/cv_cef3.png"),
          ],
        },
        {
          id: 2,
          image: require("../assets/cahierDesCharges.png"),
          title: "Cahier des charges",
          date: "2023-01-01",
          technologies: "pdf",
          link: "/pdf/cahier_des_charges_cef2024.pdf", // PDF lien
          repo: "https://github.com/example/repo2", //n'existe pas mis par défaut
          images: [
            require("@/assets/cahierDesCharges.png"),
            require("@/assets/cahierDesCharges2.png"),
            require("@/assets/cahierDesCharges3.png"),
          ],
        },
        {
          id: 3,
          image: require("../assets/dynaSite.png"), // projet le dynamisme d'un site
          title: "Dynamisme d'un Site",
          date: "2024-01-01",
          technologies: "CSS, TypeScript",
          link: "https://example.com/creation3",
          repo: "https://github.com/Thymangi/dynEspo",
          images: [
            require("@/assets/dynaSite.png"),
            require("@/assets/dynaSite2.png"),
            require("@/assets/dynaSite3.png"),
          ],
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
      this.selectedCreation = {}; // fermetrue au clique vide
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      section.scrollIntoView({ behavior: "smooth" });
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
  align-items: center; /* Center horizontalement */
  justify-content: center; /* Centrer le content verticalement */
  text-align: center; /* Centrer le text */
  margin-top: 2rem; /* ajouter de la marge au-dessus */
  min-height: 100vh; /* Assurer que la section occupe au moins toute la hauteur de la fenêtre */
}
.presentation-content {
  margin-top: 1rem; /* Reduire la marge au-dessus */
  margin-bottom: auto; /* Centrer le content verticalement */
  max-width: 800px; /* Limiter la largeur du contenu */
}

.usagers {
  display: flex;
  justify-content: center;
  flex-direction: row;
  gap: 2rem; /* espace entre les images */
  margin-top: 2rem; /* ajouter de la marge au-dessus */
}

.usager-image {
  width: 100px; /* ajuster la taille de l'image */
  height: auto;
}
.complement {
  display: flex;
  justify-content: center;
  margin-top: 2rem; /* ajouter de la marge au-dessus */
  text-align: center; /* Centrer le texte */
}
.creations {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  justify-content: center;
} /* div ensemble des création1 + créa2 + créa 3*/

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
  cursor: pointer; /* Changer le  curseur au survol */
}

.creation h3 {
  text-align: center;
  margin-top: 1rem;
  font-size: 2vw;
}

@media (max-width: 768px) {
  .creation-image {
    width: 90%;
  } /* à définir ...*/
}

.back-to-top {
  position: fixed;
  bottom: 80px; /* Ajusté pour être au-dessus du pied de page */
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
