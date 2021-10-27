<script>
export default {
  name: 'NewContactForm',
  data() {
    return {
      newContact: {
        first_name: '',
        last_name: '',
        number: '',
        personal_or_work: 'personal',
        notes: '',
      },
      validations: {
        hasFirstOrLast: () => this.newContact.first_name !== '' || this.newContact.last_name !== '',
        numberTenDigits: () => this.newContact.number.length == 10,
      },
      numberRegex: /[0-9\b]/,
    }
  },
  mounted() {
    this.$refs.numberInput.addEventListener('keydown', e => {
      let keyChar = String.fromCharCode(e.which || e.keyCode);
      if (!this.numberRegex.test(keyChar)) {
        e.preventDefault();
      }
    });
  },
  methods: {
    showNewContactForm() {
      this.$emit('showNewContactForm');
    },
    hideNewContactForm() {
      this.$emit('hideNewContactForm');
    },
    formatNumber() {
      this.newContact.number = this.newContact.number.slice(0, 3) + "-" + this.newContact.number.slice(3, 6) + "-" + this.newContact.number.slice(6);
    },
    submit() {
      this.formatNumber();
      this.$emit('submit', this.newContact);
      this.hideNewContactForm();
    },
  },
  computed: {
    isValid() {
      return this.validations.hasFirstOrLast && this.validations.numberTenDigits;
    },
    needsName() {
      return !this.validations.hasFirstOrLast;
    },
    numberIncorrect() {
      return !this.validations.numberTenDigits;
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
  .container {
    width: 50%;
    position: fixed;
    left: 25%;
    top: 20%;
    padding: 3% 0 3%;
    border: 6px solid #d04c34;
    border-radius: 8px;
    background: linear-gradient(to right bottom, #ffb933, #eee978);
    color: #564536;
  }
  .input-field {
    padding: 12px 8px 2px;
    font-size: 18px;
  }
  .title-text {
    color: #8b5e30;
  }
  .btn-row {
    display: flex;
    width: 80%;
    justify-content: space-between;
    margin: auto;
  }
  .btn {
    flex: 1;
    border-radius: 4px;
    font-weight: 600;
    font-size: 18px;
    color: white;
    width: 50%;
    cursor: pointer;
  }
  .cancel {
    background-color: grey;
    margin-right: 6px;
  }
  .submit {
    background-color: #d04c34;
    margin-left: 6px;
  }
  input, textarea {
    width: 70%;
  }
</style>

<template>
  <div class="container">
    <div class="title-text">
      <h2>Add New Contact</h2>
    </div>
    <div class="input-field">
      <input type="text" placeholder="First Name" v-model="newContact.first_name" />
    </div>
    <div class="input-field">
      <input type="text" placeholder="Last Name" v-model="newContact.last_name" />
    </div>
    <div class="input-field">
      <input type="text" ref="numberInput" maxlength="10" placeholder="Phone Number (digits only, no dashes)" v-model="newContact.number" />
    </div>
    <div class="input-field">
      <label for="personal_or_work">Personal or Work?  </label>
      <select id="personal_or_work" name="personal_or_work" v-model="newContact.personal_or_work">
        <option value="personal">Personal</option>
        <option value="work">Work</option>
      </select>
    </div>
    <div class="input-field">
      <textarea placeholder="Notes" rows="4" v-model="newContact.notes" />
    </div>
    <div class="btn-row input-field">
      <div class="btn cancel" @click="hideNewContactForm">Cancel</div>
      <div class="btn submit" @click="submit">Submit</div>
    </div>
  </div>
</template>