<template>
  <div class="overlay">
    <div class="modal-text event">
      <ul style="color: #000 !important">
        <li>© 2011 – 2019</li>
        <li>PWA <a href="https://publishing-events.com" target="_blank">publishing-events.com</a></li>
        <li>
          an
          <a href="https://oyen.de" target="_blank">oyen.de</a> Service
        </li>
        <li>
          <a href="https://oyen.de/impressum" target="_blank">Impressum</a>
        </li>
        <li>
          <a href="https://oyen.de/datenschutz" target="_blank">Datenschutz</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["event"]
};
</script>

<style scoped>
/* modal animation */
.modal-top-enter-active,
.modal-top-leave-active {
  transform: translateY(-100%);
}
.modal-top-enter,
.modal-top-leave-to {
  transform: translateY(-100%);
}

.shadow-mx {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25) !important;
}

.event {
  width: auto;
  height: auto;
  display: flex;
  justify-content: center;
  background: #fff !important;
  color: #000 !important;
  padding-top: 10px;
  margin: 0;
}
.event > ul > li {
  display: block;
  text-align: center;
  line-height: 1.8;
}

.overlay {
  height: 100%;
  width: 100%;
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999 !important;
  top: 0;
  left: 0;
  background: #fff;
  overflow: hidden !important;
  transition: 0.3s;
}

.overlay::-webkit-scrollbar {
  /* This is the magic bit for WebKit */
  display: none;
}

.overlay .modal-text {
  background: #fff;
  color: #fff !important;
  font-size: 0.94rem;
}
</style>
