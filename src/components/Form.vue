<template>
  <div class="form">
    <div class="container">
      <h2>Contact Us</h2>
      <div class="form_wrapper">
        <form action="http://httpbin.org/post" method="POST" class="form_item" @submit="checkForm">
          <p class="input-text" v-bind:class="{ error: hasErrorName }">
            <label for="">Name</label>
            <input type="text" id="input-text" v-model="name" >
          </p>
          <p class="input-text" v-bind:class="{ error: hasErrorPhone }">
            <label for="">Phone</label>
            <the-mask mask="+38093#######" value="+38093" type="tel" v-model="phone"></the-mask>
          </p>
          <p class="input-text" v-bind:class="{ error: hasErrorEmail }">
            <label for="">Email</label>
            <input type="email" name="" id="" v-model="email">
          </p>
          <p class="input-checkbox" v-bind:class="{ error: hasErrorCheck }">
            <input type="checkbox" name="" id="" v-model="isAgree" >
            <label for="">I agree the processing of personal data</label>
          </p>
          <input type="submit" value="Get in touch" class="input-submit" :disabled="submitted">
        </form>
        <div class="form_item">
          <p>Please tell us more about your request and give us info about your company and country.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data () {
    return {
      name: null,
      phone: null,
      email: null,
      isAgree: false,
      hasErrorName: false,
      hasErrorPhone: false,
      hasErrorEmail: false,
      hasErrorCheck: false,
      submitted: false
    }
  },
  methods: {
    checkForm: function (e) {
      e.preventDefault();

      this.hasErrorName = !(this.name && this.validName(this.name));

      this.hasErrorPhone = !(this.phone && this.validPhone(this.phone));

      this.hasErrorEmail = !(this.email && this.validEmail(this.email));

      this.hasErrorCheck = !this.isAgree;

      if (!this.hasErrorName && !this.hasErrorPhone && !this.hasErrorEmail && !this.hasErrorCheck) {
        this.submitted = true;
        return true;
      }
      
    },
    validName: function (name) {
      let regName = /^[A-Za-z ]+$/;
      return regName.test(name);
    },
    validPhone: function (phone) {
      return phone.length === 7;
    },
    validEmail: function (email) {
      var regEmail = /^(\w\.?)+@{1}([A-Za-z]\D+)+(\.{1}[a-zA-Z]{2,6})+$/;
      return regEmail.test(email);
    }
  }
}

</script>
