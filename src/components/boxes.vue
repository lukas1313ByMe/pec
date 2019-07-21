<template>
  <div>
    <div
      :style="{background: '#' + item.background, color: '#' + item.color}"
      v-for="item in data"
      :key="item.Id"
      class="box-wrapper"
    >
      <div class="imgbox">
        <span class="box-header" v-html="item.header"></span>
        <a target="_blank" :href="item.URL">
          <img :src="item.img_link" v-if="item.img_link" alt>
        </a>
        <span class="sub-text" v-html="item.text"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["data"]
};
</script>


<style>
.box-wrapper {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-gap: 20px 0;
  grid-auto-rows: 100%;
  margin: 0 11px 11px 0;
  grid-template-areas:
    ". a a ."
    ". a a .";
  border-radius: 4px;
}
/* default class */
.imgbox {
  display: flex;
  flex-direction: column;
  justify-self: center;
  justify-content: center;
  /* min-width: 130px; */
  max-width: 260px;
  padding: 10px;
  padding-top: 0;
  height: auto;
}

.box-header {
  padding: 10px;
  padding-top: 0;
  font-size: 1.1rem;
  font-weight: 600;
  text-align: left;
  width: 100%;
}
.sub-text {
  text-align: left;
}
img {
  width: 100%;
  object-fit: contain;
  margin-bottom: 10px;
}

@media screen and (max-width: 600px) {
  .box-wrapper {
    margin: 11px;
  }
}
</style>
