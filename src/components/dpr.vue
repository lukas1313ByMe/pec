e<template>
  <div class="dpr-wrapper">
    <div v-for="item in items" :key="item.Id" class="dpr-card">
      <!-- <div v-if="item.dpr_issue_topics">{{item.dpr_issue_topics}}</div> -->
      <span class="date-text">{{item.dpr_issue_num_year}}</span>
      <a target="_blank" :href="item.dpr_issue_pdf_url">
        <img :src="item.dpr_issue_img_url" alt="image">
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["items"]
};
</script>

<style>
.dpr-wrapper {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  flex-direction: wrap;
  flex-wrap: wrap;
}
.dpr-card {
  width: 120px;
  height: 171px;
  margin: 14px 4px 8px 4px;
}
.date-text {
  display: flex;
  justify-content: flex-start;
  color: grey;
  font-size: 12.8px;
}

@media screen and (max-width: 600px) {
  .dpr-wrapper {
    width: 100%;
    justify-content: center;
  }
  .dpr-card {
    width: 110px;
    margin-top: 0;
  }
}
/* iphone x */
@media screen and (min-width: 375px) and (max-width: 375px) {
  .dpr-wrapper {
    width: 100%;
    justify-content: center;
  }
  .dpr-card {
    width: 100px;
    margin-top: 0;
  }
}
</style>

