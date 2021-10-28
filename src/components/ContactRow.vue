<script>
export default {
  name: 'ContactRow',
  props: ['infoObj', 'divider', 'contactIndex'],
  data() {
    return {
      selected: false,
      editMode: false,
      updatedInfoObj: {},
      window: {
        height: 0,
        width: 0,
      },
    }
  },
  computed: {
    hasDivider() {
      return this.divider == true;
    },
    isMobileWidth() {
      return this.window.width < 716;
    },
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
    toggleSelection() {
      this.selected = !this.selected;
    },
    deleteContact() {
      this.$emit('deleteContact');
    },
    stripNumberDashes() {
      this.updatedInfoObj.number = this.updatedInfoObj.number.slice(0, 3) + this.updatedInfoObj.number.slice(4, 7) + this.updatedInfoObj.number.slice(8);
    },
    formatNumber() {
      this.updatedInfoObj.number = this.updatedInfoObj.number.slice(0, 3) + "-" + this.updatedInfoObj.number.slice(3, 6) + "-" + this.updatedInfoObj.number.slice(6);
    },
    editContact() {
      this.stripNumberDashes();
      this.editMode = true;
    },
    updateContact() {
      this.formatNumber();
      this.editMode = false;
      this.$emit('updateContact', this.contactIndex, this.updatedInfoObj);
    },
    setIndex() {
      this.$emit('setCurrentIndex', this.contactIndex);
    },
  },
  created() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize);
  },
  mounted() {
    // copy infoObj to updatedInfoObj
    for (const property in this.infoObj) {
      this.updatedInfoObj[property] = this.infoObj[property];
    }
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
    position: relative;
    padding: 12px 0;
    display: flex;
    flex-wrap: wrap;
    font-weight: 700;
    align-items: center;
    justify-content: space-between;
    text-align: start;
  }
  .contact-info {
    cursor: pointer;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .contact-info:hover {
    text-decoration: underline;
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
  .flex-group2 {
    flex: 2 2 350px;
    display: flex;
  }
  .flex-group3 {
    flex: 3 3 350px;
    display: flex;
  }
  .extra-mobile-padding {
    padding: 0 0 0 6%;
  }
  .action-row {
    display: flex;
    height: 22px;
    width: 30px;
    justify-content: space-evenly;
  }
  .action-item {
    padding: 0 3px;
    cursor: pointer;
  }
  .action-item-img {
    height: 100%;
  }
</style>

<template>
  <div class="contact-row" v-bind:class="{ 'bottom-divider' : hasDivider, 'selected' : selected }">
    <div class="flex-group2">
      <span class="flex1"><input type="checkbox" @click="toggleSelection" /></span>

      <span v-if="!editMode" class="contact-info flex2" @click="setIndex">{{ infoObj.last_name }}</span>
      <div v-else class="contact-info flex2"><input type="text" v-model="updatedInfoObj.last_name" /></div>

      <span v-if="!editMode" class="contact-info flex2" @click="setIndex">{{ infoObj.first_name }}</span>
      <div v-else class="contact-info flex2"><input type="text" v-model="updatedInfoObj.first_name" /></div>
    </div>

    <div class="flex-group3" v-bind:class="{ 'extra-mobile-padding' : isMobileWidth }">
      <span v-if="!editMode" class="contact-info flex3" @click="setIndex">{{ infoObj.number }}</span>
      <div v-else class="contact-info flex3"><input type="text" maxlength="10" v-model="updatedInfoObj.number" /></div>

      <span v-if="!editMode" class="contact-info flex2" @click="setIndex">{{ infoObj.personal_or_work == "work" ? "work" : "personal" }}</span>
      <div v-else class="contact-info flex2">
        <select id="personal_or_work" name="personal_or_work" v-model="updatedInfoObj.personal_or_work">
          <option value="personal">Personal</option>
          <option value="work">Work</option>
        </select>
      </div>

      <div v-if="selected" class="action-row contact-info flex1">
        <div v-show="!editMode" class="action-item" @click="editContact">
          <img class="action-item-img" src="../assets/edit_icon.png" />
        </div>
        <div v-show="editMode" class="action-item" @click="updateContact">
          <img class="action-item-img" src="../assets/checkmark.png" />
        </div>
        <div class="action-item" @click="deleteContact">
          <img class="action-item-img" src="../assets/delete_icon.png" />
        </div>
      </div>
      <div v-else class="contact-info flex1"></div>
    </div>
  </div>
</template>