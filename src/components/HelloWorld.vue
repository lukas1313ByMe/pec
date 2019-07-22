<template>
  <div class="wrapper-e">
    <div class="boxes e">
      <l-events style="margin-top: 60px; width: 100%;"/>
    </div>
  </div>
</template>

<script>
import lEvents from "@/components/events";

export default {
  name: "HelloWorld",
  components: {
    lEvents
  }
};
</script>

<style>
.wrapper-e {
  padding-top: 20px;
  display: grid;
  grid-template-columns: 0.3fr 0.6fr 0.3fr;
  grid-gap: 12px;
}

.lh {
  grid-column: 1 / span 4;
  grid-row: 1 / span 2;
}

.e {
  grid-column: 2 / span 1;
  grid-row: 2;
}

@media screen and (min-width: 600px) and (max-width: 800px) {
  .wrapper-e {
    padding-top: 20px;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 12px;
  }
  .lh {
    grid-column: 1 / span 1;
    grid-row: 1 / span 2;
  }
  .event {
    height: auto;
  }
}

@media screen and (max-width: 600px) {
  .wrapper-e {
    padding-top: 0;
    display: grid;
    grid-template-columns: 100%;
    grid-gap: 0;
  }
  .lh {
    grid-column: 1 / span 4;
    grid-row: 1 / span 2;
  }
  .e {
    display: flex;
    justify-content: center;
    grid-column: 1 / span 4;
    grid-row: 3;
  }
  .events {
    justify-content: flex-start;
    justify-content: center;
  }
  .event {
    width: 140px;
    height: 140px;
    color: #202124 !important;
  }
}
/* ipad portrai */
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) {
  .wrapper-e {
    padding-top: 20px;
    display: grid;
    grid-template-columns: 100%;
    grid-gap: 12px;
  }
  .lh {
    grid-column: 1 / span 2;
    grid-row: 1 / span 2;
  }
  .e {
    display: flex;
    grid-column: 1 / span 2;
    grid-row: 3;
    width: 100%;
  }
  .events {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
  }
  .event {
    width: 240px !important;
    height: 160px;
    color: #202124 !important;
  }
  .header-filter {
    width: 100%;
  }
  input:checked + .slider:before {
    -webkit-transform: translateX(274px) !important;
    -ms-transform: translateX(274px) !important;
    transform: translateX(274px) !important;
  }
}

/* ipad lanmdscape */
@media only screen and (min-device-width: 1024px) and (max-device-width: 1024px) {
  .header-filter {
    width: 100%;
  }
}

@media screen and (min-width: 1200px) and (max-width: 1400px) {
  .wrapper-e {
    padding-top: 20px;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 12px;
  }

  .lh {
    grid-column: 1 / span 4;
    grid-row: 1 / span 2;
  }

  .e {
    display: flex;
    justify-content: center;
    grid-column: 1 / span 4;
    grid-row: 3;
  }
  .header-filter {
    width: 100%;
  }
  input:checked + .slider:before {
    -webkit-transform: translateX(284px) !important;
    -ms-transform: translateX(284px) !important;
    transform: translateX(284px) !important;
  }
}

@media screen and (min-width: 1200px) {
  .lh {
    grid-column: 1 / span 4;
    grid-row: 1 / span 2;
  }
  .header-filter {
    width: 100%;
  }
  .event {
    width: 258px !important;
  }
}

/* ----------- iPad Pro ----------- */
/* Portrait */
@media only screen and (min-width: 1024px) and (max-height: 1366px) and (orientation: portrait) and (-webkit-min-device-pixel-ratio: 1.5) {
  .event {
    width: 160px;
    height: 160px;
    color: #202124 !important;
  }
  .header-filter {
    width: 100%;
  }
  .e {
    display: flex;
    grid-column: 1 / span 2;
    grid-row: 3;
    width: 100%;
  }
}

.boxes {
  color: #fff;
  padding: 1em;
}

* {
  box-sizing: border-box;
}

html,
body {
  background: #fff;
  overflow-x: hidden;
  padding: 0;
  margin: 0;
}

a {
  text-decoration: none;
}
</style>
