<script>
export default {
  name: 'ContactRow',
  props: ['infoObj', 'divider', 'deleteFunc', 'selectFunc'],
  data() {
    return {
      selected: false,
    }
  },
  computed: {
    hasDivider() {
      return this.divider == true;
    },
  },
  methods: {
    toggleSelection() {
      this.selected = !this.selected;
    },
  }
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
  .action-row {
    position: absolute;
    right: 38px;
    display: flex;
    height: 25px;
    width: 30px;
    justify-content: space-between;
  }
  .action-item {
    padding: 0 2px;
  }
  .action-item-img {
    height: 100%;
  }
</style>

<template>
  <div class="contact-row" v-bind:class="{ 'bottom-divider' : hasDivider, 'selected' : selected }">
    <span class="flex1"><input type="checkbox" @click="toggleSelection" /></span>
    <span class="contact-info flex2">{{ infoObj.last_name }}</span>
    <span class="contact-info flex2">{{ infoObj.first_name }}</span>
    <span class="contact-info flex3">{{ infoObj.number }}</span>
    <span class="contact-info flex2">{{ infoObj.personal_or_work == "work" ? "work" : "personal" }}</span>
    <div v-show="selected" class="action-row">
      <div class="action-item">
        <img class="action-item-img" src="../assets/edit_icon.png" />
      </div>
      <div class="action-item">
        <img class="action-item-img" src="../assets/delete_icon.png" />
      </div>
    </div>
  </div>
</template>