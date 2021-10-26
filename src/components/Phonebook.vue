<script>
import allContacts from "../contacts.json";
import ContactRow from "./ContactRow";
import NewContactForm from "./NewContactForm";

export default {
  name: 'Phonebook',
  components: { ContactRow, NewContactForm },
  data() {
    return {
      contacts: [],
      newContactFormVisible: false,
    };
  },
  mounted() {
    this.contacts = JSON.parse(JSON.stringify(allContacts));
  },
  methods: {
    deleteSingleContact(index) {
      this.contacts.splice(index, 1);
    },
    toggleSelect(index) {
      this.contacts[index].isSelected = !this.contacts[index].isSelected;
    },
    showNewContactForm() {
      this.newContactFormVisible = true;
    },
    hideNewContactForm() {
      this.newContactFormVisible = false;
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
<style>
  .header {
    max-width: 875px;
    width: 100%;
    height: 105px;
    display: flex;
    padding: 0 3%;
    position: relative;
    align-items: center;
    justify-content: space-between;
    background: linear-gradient(to right, #8b5e30, #564536);
  }
  .title {
    font-weight: 900;
    color: var(--yellow);
    font-size: 24px;
    color: #eee978;
  }
  .decoration {
    font-size: 30px;
  }
  .control-row {
    position: relative;
    display: flex;
    justify-content: space-between;
    width: 100%;
    max-width: 875px;
    padding: 24px 3% 6px;
    background: linear-gradient(to right, #eee978, #ffb933);
    color: #564536;
    font-weight: 600;
    text-align: start;
    text-decoration: underline;
  }
  .add-new-btn {
    border: 2px solid #564536;
    border-radius: 8px;
    width: 50px;
    height: 50px;
    background: linear-gradient(to right bottom, #d04c34, #ffb933);
    line-height: 50px;
    cursor: pointer;
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
  .new-contact-form {
    display: none;
  }
  .show-form {
    display: inline;
  }
</style>

<template>
  <div>
    <div class="header">
      <div class="decoration">🎃</div>
      <div class="title">Phonebook</div>
      <div class="decoration">
        <div class="add-new-btn" @click="showNewContactForm">+</div>
      </div>
    </div>
    <div class="control-row">
      <span class="control-header flex1">
        <input type="checkbox" />
      </span>
      <span class="control-header flex2">Last</span>
      <span class="control-header flex2">First</span>
      <span class="control-header flex3">#</span>
      <span class="control-header flex2">Type</span>
    </div>
    <div v-for="(contact, index) in contacts" :key="contact.number">
      <ContactRow :infoObj="contact" :divider="index !== 0" @deleteContact="deleteSingleContact(index)" />
    </div>
    <NewContactForm
      class="new-contact-form"
      v-bind:class="{ 'show-form' : newContactFormVisible }"
      @showNewContactForm="showNewContactForm"
      @hideNewContactForm="hideNewContactForm"
    />
  </div>
</template>