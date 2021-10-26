<script>
export default {
  name: 'NewContactForm',
  data() {
    return {
      first_name: '',
      last_name: '',
      number: '',
      personal_or_work: 'personal',
      notes: '',
      validations: {
        hasFirstOrLast: () => this.first_name !== '' || this.last_name !== '',
        numberTenDigits: () => this.number.length == 10,
      }
    }
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
    margin: auto;
    height: 70%;
    width: 50%;
    position: fixed;
    border: 4px solid #d04c34;
    border-radius: 8px;
  }
</style>

<template>
  <div class="container">
    <div class="input-field">
      <input type="text" placeholder="First Name" v-model="first_name" />
    </div>
    <div class="input-field">
      <input type="text" placeholder="Last Name" v-model="last_name" />
    </div>
    <div class="input-field">
      <input type="text" placeholder="Phone Number" v-model="number" />
    </div>
    <div class="input-field">
      <label for="personal_or_work">Personal or Work?</label>
      <select id="personal_or_work" name="personal_or_work">
        <option value="personal">Personal</option>
        <option value="work">Work</option>
      </select>
    </div>
    <div class="input-field">
      <input type="text" placeholder="Notes" v-model="notes" />
    </div>
  </div>
</template>