<template>
  <div class="header-wrapper">
    <div class="header-filter">
      <label class="switch">
        <input
          type="checkbox"
          v-bind:checked="checked"
          v-on:change="$emit('change', $event.target.checked)"
          id="togBtn"
        >
        <div class="slider round"></div>
      </label>
    </div>
    <div class="text-header burger-menu">
      <div :class="{'open' : openToggle}" @click="toggle" id="burger" class="hamburger">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
    <transition name="modal-top">
      <l-modal v-if="openToggle"/>
    </transition>
  </div>
</template>

<script>
import lModal from "@/components/modalHeader";
export default {
  components: {
    lModal
  },
  model: {
    prop: "checked",
    event: "change"
  },
  props: {
    checked: Boolean
  },
  data() {
    return {
      openToggle: false,
      buttonState: "Online"
    };
  },
  mounted() {
    document.addEventListener("keydown", e => {
      if (e && e.keyCode === 27) {
        this.openToggle = false;
      }
    });
  },
  methods: {
    toggle() {
      this.openToggle = !this.openToggle;
    }
  }
};
</script>


<style>
/* switch buttons */
.switch {
  position: relative;
  display: flex;
  justify-content: flex-start;
  width: 320px;
  height: 44px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #37474F;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 34px;
  width: 34px;
  left: 6px;
  bottom: 6.6px;
  background-image: url("https://www.oyen.de/img/logo.png"); /* The image used */
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked + .slider {
  background-color: #337ab7;
}

input:focus + .slider {
  box-shadow: 0 0 1px #37474F;
}

input:checked + .slider:before {
  -webkit-transform: translateX(258px);
  -ms-transform: translateX(258px);
  transform: translateX(258px);
}

.slider:after {
  content: "Offline publishing-events.com";
  width: 100%;
  color: white;
  display: block;
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  font-size: 13px;
  letter-spacing: 1.2;
  font-family: Verdana, sans-serif;
}

input:checked + .slider:after {
  content: "Online publishing-events.com";
}

/*--------- END --------*/

/* filter */
.header-filter {
  display: flex;
  flex-direction: wrap;
  justify-content: center;
  position: fixed;
  color: #fff;
  top: 2.4%;
  width: 80%;
  left: 10px;
}
.header-filter > button {
  border: none;
  background: #fff;
  width: 60px;
}

.header-wrapper {
  width: 100%;
  height: 80px;
  color: #fff;
  background: #fff;
  position: fixed;
  top: 0;
  left: 0;
  margin: 0;
  z-index: 9999999;
}
.inner-wrapper-header {
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-content: space-around;
}
.burger-menu {
  display: flex;
  justify-content: flex-end;
  padding-right: 4%;
}
.text-header {
  display: flex;
  align-items: center;
  width: 100%;
  height: 60px;
}

.text-header:first-child {
  padding-left: 10px;
}

.big {
  width: 100%;
}
.big.bigger {
  font-size: 1.2rem;
  font-weight: bold;
}

/* overlay for impressum, .... */
.overlay-header {
  height: 100%;
  width: 100%;
  position: fixed;
  /* z-index: 9999; */
  top: 0;
  left: 0;
  background: #fff;
  overflow: hidden !important;
  transition: 0.3s;
}

a {
  color: #337ab7 !important;
}

/* animation hamburger */
.hamburger {
  cursor: pointer;
  transform: rotate(0);
  transition: 0.5s ease-in-out;
  -webkit-transform: rotate(0);
  width: 40px;
  height: 8px;
  z-index: 999999;
}
.hamburger div {
  background: #202124;
  border-radius: 9px;
  display: block;
  height: 4.4px;
  right: 0;
  position: absolute;
  transform: rotate(0);
  transition: 0.25s ease-in-out;
  -webkit-transform: rotate(0);
  width: 100%;
}
.hamburger div:nth-child(1) {
  top: 0;
}
.hamburger div:nth-child(2),
.hamburger div:nth-child(3) {
  top: 13px;
}
.hamburger div:nth-child(4) {
  top: 26px;
}
.hamburger.open div:nth-child(1),
.hamburger.open div:nth-child(4) {
  left: 50%;
  top: 30px;
  width: 0%;
}
.hamburger.open div:nth-child(2) {
  background: #bbb;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}
.hamburger.open div:nth-child(3) {
  background: #bbb;
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

@media screen and (max-width: 375px) {
  .hamburger {
    height: 13px;
  }
}
@media screen and (max-width: 360px) {
  input:checked + .slider:before {
    -webkit-transform: translateX(212px);
    -ms-transform: translateX(212px);
    transform: translateX(212px);
  }
}
</style>
