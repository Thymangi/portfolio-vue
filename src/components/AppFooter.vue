<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="social-icons">
        <a href="https://twitter.com/yourprofile" target="_blank">
          <img src="@/assets/twitter.png" alt="Twitter" />
        </a>
        <a href="https://linkedin.com/in/yourprofile" target="_blank">
          <img src="@/assets/linkedin.png" alt="LinkedIn" />
        </a>
        <a href="https://github.com/yourprofile" target="_blank">
          <img src="@/assets/github.png" alt="GitHub" class="github-icon" />
        </a>
      </div>
      <div class="footer-text">Dernière mise à jour : {{ lastUpdated }}</div>
    </div>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      lastUpdated: new Date().toLocaleDateString(),
    };
  },
};
</script>

<style scoped>
.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #7d5bf7;
  color: white;
  text-align: center;
  padding: 1rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.footer-content {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

.social-icons {
  display: flex;
  gap: 1rem;
  margin-bottom: 0.5rem;
}

.social-icons img {
  width: 24px;
  height: 24px;
}

.github-icon {
  width: 20px; /* Reduced size for GitHub icon */
  height: 20px;
}
.social-icons img:hover {
  transform: scale(1.2); /* Scale the icon */
  filter: brightness(1.2); /* Increase brightness */
}

.footer-text {
  font-size: 0.9rem;
}
</style>
