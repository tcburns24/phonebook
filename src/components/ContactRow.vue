<script>
export default {
  name: 'ContactRow',
  props: ['infoObj'],
  data() {
    return {}
  },

}
</script>

<!--
COLOR THEME 
orange: #ffb933
red:    #d04c34
black:  #564536
brown: 	#8b5e30
yellow: #eee978
-->
<style scoped>
  .contact-row {
    max-width: 100%;
    position: relative;
    padding: 1% 0;
    display: flex;
    border: 1px solid #8b5e30;
    font-weight: 700;
  }
</style>

<template>
  <div class="contact-row">
    <span><input type="checkbox" /></span>
    <span class="contact-info">{{ infoObj.last_name }}</span>
    <span class="contact-info">{{ infoObj.first_name }}</span>
    <span class="contact-info">{{ infoObj.number }}</span>
    <span class="contact-info">{{ infoObj.type }}</span>
  </div>
</template>