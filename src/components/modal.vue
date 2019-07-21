<template>
  <div class="overlay">
    <div class="modal-text event">
      <div class="event-circle-box">
        <div
          style="color: #fff"
          :style="{ background: event.e_color + '!important' }"
          class="event-circle"
        >{{ event.e_counter }}</div>
      </div>
      <ul style="color: #000 !important; padding-top: 20px;">
        <li class="event-text">{{event.e_date}} {{event.e_location}}</li>
        <li class="event-text" style="padding-top: 3px">{{event.e_name}}</li>
        <li style="padding-top: 10px" class="modal-sub-text modal-desc">{{event.e_description}}</li>
      </ul>
    </div>
    <button class="c-button" @click="$emit('close')">X</button>
    <div class="spacer">
      <button class="a-button green shadow-max">
        <a :href="event.e_save_the_date">Datum Speichern</a>
      </button>
      <button class="a-button purple shadow-max">
        <a target="_blank" :href="event.e_url">Veranstalter</a>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["event"]
};
</script>
<style scoped>
/* IMPORTANT TO USE `scope` IN STYLE ABOVE, IF NOT CLASSES WILL BE OVERWRITTEN*/
a {
  color: #fff !important;
}

.shadow-mx {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25) !important;
}

.event-circle-box {
  margin: 10px;
}

.modal-sub-text {
  font-size: 1.04rem;
  font-weight: 400;
  padding: 3px 0;
}

.modal-sub-text a {
  color: #1782df;
}

.modal-desc {
  height: 600px !important;
  overflow: auto !important;
}

.event {
  width: auto;
  height: auto;
  background: #fff !important;
  color: #000 !important;
  padding-top: 30.2px;
}
.event > ul > li {
  display: block;
}

.event-text {
  font-size: 1.12rem !important;
}

.overlay {
  height: 100%;
  width: 100%;
  position: fixed;
  z-index: 999999999;
  top: 0;
  left: 0;
  background: #fff;
  overflow-x: hidden !important;
  transition: 0.3s;
}

.overlay::-webkit-scrollbar {
  /* This is the magic bit for WebKit */
  display: none;
}

.overlay .modal-text {
  background: #fff;
  color: #fff !important;
  font-size: 0.86rem;
}
/* closing button 'x' */
.overlay .c-button {
  width: 44px !important;
  position: fixed;
  top: 0;
  font-size: 1.44rem;
  right: 0;
  z-index: 9999;
  height: 40px;
  color: #202124;
  cursor: pointer;
  border: none;
  background: transparent;
}
.overlay .a-button {
  height: 46px;
  width: 140px;
  color: #fff;
  border: none;
  border-radius: 100px;
  font-weight: 400;
  font-size: 14px;
  letter-spacing: 0.6px;
}
.overlay .a-button.green {
  background: #37474F;
}
.overlay .a-button.purple {
  background: #37474F;
}
.spacer {
  position: fixed;
  margin: 0;
  bottom: 16px;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: flex-end;
}
</style>
