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
      window: {
        height: 0,
        width: 0,
      },
      numberRegex: /[0-9\b]/,
    }
  },
  created() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize);
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
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
    showNewContactForm() {
      this.$emit('showNewContactForm');
    },
    hideNewContactForm() {
      this.$refs.errors.innerText = '';
      this.$emit('hideNewContactForm');
    },
    formatNumber() {
      this.newContact.number = this.newContact.number.slice(0, 3) + "-" + this.newContact.number.slice(3, 6) + "-" + this.newContact.number.slice(6);
    },
    submit() {
      if (!this.validations.hasFirstOrLast()) {
        this.$refs.errors.innerText = 'Contacts must have a first or last name';
      } else if (!this.validations.numberTenDigits()) {
        this.$refs.errors.innerText = 'Phone numbers must be 10 digits';
      } else {
        this.$refs.errors.innerText = '';
        this.formatNumber();
        this.$emit('submit', this.newContact);
        this.hideNewContactForm();
      }
    },
  },
  computed: {
    isMobileWidth() {
      return this.window.width < 716;
    },
    isValid() {
      return this.validations.hasFirstOrLast() && this.validations.numberTenDigits();
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
    text-align: center;
  }
  .mobile {
    width: 90%;
    position: fixed;
    left: 2%;
    top: 10%;
    padding: 3% 0 3%;
    border: 6px solid #d04c34;
    border-radius: 8px;
    background: linear-gradient(to right bottom, #ffb933, #eee978);
    color: #564536;
    text-align: center;
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
  .errors {
    color: #d04c34;
    font-weight: 700;
  }
</style>

<template>
  <div v-bind:class="{ 'mobile' : isMobileWidth, 'container' : !isMobileWidth }">
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
    <div class="errors" ref="errors"></div>
    <div class="btn-row input-field">
      <button class="btn cancel" @click="hideNewContactForm">Cancel</button>
      <button class="btn submit" @click="submit">Submit</button>
    </div>
  </div>
</template>