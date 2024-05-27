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
          <img :src="image" :alt="'Image ' + (index + 1)" />
        </div>
        <button class="carousel-control prev" @click="prevImage">‹</button>
        <button class="carousel-control next" @click="nextImage">›</button>
      </div>
      <p><strong>Date de création :</strong> {{ creation.date }}</p>
      <p>
        <strong>Technologies utilisées :</strong> {{ creation.technologies }}
      </p>
      <p v-if="creation.link">
        <strong>Visitez le site ou fichier :</strong>
        <a :href="creation.link" target="_blank">{{ creation.link }}</a>
      </p>
      <p v-if="creation.repo">
        <strong>Repository GitHub :</strong>
        <a :href="creation.repo" target="_blank">{{ creation.repo }}</a>
      </p>
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
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  position: relative;
  max-width: 500px;
  width: 90%;
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

.carousel {
  position: relative;
  width: 100%;
  margin-bottom: 1rem;
}

.carousel-item {
  display: none;
  text-align: center;
}

.carousel-item.active {
  display: block;
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
