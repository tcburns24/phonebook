<script>
export default {
  name: 'ContactRow',
  props: ['infoObj', 'divider'],
  data() {
    return {
      
    }
  },
  computed: {
    hasDivider() {
      return this.divider == true;
    },
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
    width: 100%;
    max-width: 875px;
    position: relative;
    padding: 3px 3%;
    display: flex;
    font-weight: 700;
    align-items: center;
    justify-content: space-between;
    text-align: start;
  }
  .bottom-divider {
    border-top: 1px solid #8b5e30;
  }
  .selected {
    background: linear-gradient(to right top, #ffb933, #d04c34);
  }
  .flex1 {
    flex: 1;
  }
  .flex2 {
    flex: 2;
  }
  .flex3 {
    flex: 3;
  }
</style>

<template>
  <div class="contact-row" v-bind:class="{ 'bottom-divider' : hasDivider, 'selected' : infoObj.isSelected }">
    <span class="flex1"><input type="checkbox" /></span>
    <span class="contact-info flex2">{{ infoObj.last_name }}</span>
    <span class="contact-info flex2">{{ infoObj.first_name }}</span>
    <span class="contact-info flex3">{{ infoObj.number }}</span>
    <span class="contact-info flex2">{{ infoObj.personal_or_work == "work" ? "work" : "personal" }}</span>
  </div>
</template>