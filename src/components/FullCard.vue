<script>
export default {
  name: 'FullCard',
  props: ['contactObj'],
  data() {
    return {}
  },
  methods: {
    hide() {
      this.$emit('hideFullCard');
    },
  }
}
</script>

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
  .close-x {
    position: absolute;
    top: 8px;
    right: 8px;
    color: black;
    font-weight: 900;
    font-size: 18px;
    height: 28px;
    width: 28px;
    cursor: pointer;
  }
  img {
    height: 100%;
    object-fit: contain;
  }
</style>

<template>
  <div class="container">
    <div class="close-x" @click="hide">
      <img src="../assets/close_x.png" />
    </div>
    <div class="title-text">
      <h2>{{ contactObj.first_name }} {{ contactObj.last_name }}</h2>
    </div>
    
    <div class="input-field">
      <textarea placeholder="Notes" rows="4" v-model="contactObj.notes" />
    </div>
  </div>
</template>