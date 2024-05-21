<template>
  <div class="modal" v-if="visible">
    <div class="modal-content" @click.stop>
      <span class="close" @click="close">&times;</span>
      <h2>{{ creation.title }}</h2>
      <p>Date de création : {{ creation.date }}</p>
      <p>Technologies : {{ creation.technologies }}</p>
      <a :href="creation.link" target="_blank">Voir le site</a>
      <a :href="creation.repo" target="_blank">Repository GitHub</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visible: Boolean,
    creation: Object,
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background: #fff;
  padding: 2rem;
  border-radius: 10px;
  position: relative;
  color: black; /* Text color is black */
}
.close {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
  font-size: 1.5rem;
}
</style>
