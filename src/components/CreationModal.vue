<template>
  <div v-if="visible" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <button class="close-button" @click="closeModal">X</button>
      <h2>{{ creation.title }}</h2>
      <div class="carousel">
        <div
          v-for="(image, index) in creation.images"
          :key="index"
          class="carousel-item"
          :class="{ active: index === activeIndex }"
        >
          <img
            :src="image"
            :alt="'Image ' + (index + 1)"
            class="carousel-image"
          />
        </div>
        <button class="carousel-control prev" @click="prevImage">‹</button>
        <button class="carousel-control next" @click="nextImage">›</button>
      </div>
      <div class="creation-details">
        <p><strong>Date de création :</strong> {{ creation.date }}</p>
        <p>
          <strong>Technologies utilisées :</strong> {{ creation.technologies }}
        </p>
        <p v-if="creation.link">
          <strong>Visitez le site ou fichier :</strong>
          <a :href="getLink(creation.link)" target="_blank">Ouvrir le PDF</a>
        </p>
        <p v-if="creation.repo">
          <strong>Repository GitHub :</strong>
          <a :href="creation.repo" target="_blank">{{ creation.repo }}</a>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visible: {
      type: Boolean,
      required: true,
    },
    creation: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      activeIndex: 0,
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    prevImage() {
      this.activeIndex =
        (this.activeIndex + this.creation.images.length - 1) %
        this.creation.images.length;
    },
    nextImage() {
      this.activeIndex = (this.activeIndex + 1) % this.creation.images.length;
    },
    getLink(file) {
      return this.isExternalLink(file)
        ? file
        : `${process.env.BASE_URL}${file}`;
    },
    isExternalLink(url) {
      return /^(http|https):/.test(url);
    },
  },
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000; /* Assurer que le modal est au-dessus des autres éléments */
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  position: relative;
  max-width: 800px;
  width: 90%;
  height: 90vh; /* ajuste la hauteur du modal à l'écran */
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-y: auto; /* Activer le défilement pour le contenu modal */
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}
h2 {
  color: black;
  margin-bottom: 10px;
  text-align: center;
}

.creation-details {
  text-align: center;
  width: 100%;
  margin-bottom: 10px;
  color: black;
}

.creation-details p {
  margin: 0.5rem 0;
}

.creation-details a {
  color: #42b983;
  text-decoration: none;
}
.carousel {
  position: relative;
  width: 100%;
  margin-bottom: 1rem;
  flex: 1; /* Faire en sorte que le carrousel occupe l'espace restant */
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
  height: calc(100% - 180px); /* Ajuste la hauteur */
}

.carousel-item {
  display: none;
  text-align: center;
  height: 100%; /* Garantir que l'iteme prend tout l'espace */
}

.carousel-item.active {
  display: flex; /* Utiliser flex pour centrer l'image */
  justify-content: center;
  align-items: center;
}
.carousel-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; /* Garantit que l'image couvre le conteneur */
}

.carousel-control {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

.carousel-control.prev {
  left: 10px;
}

.carousel-control.next {
  right: 10px;
}
</style>
