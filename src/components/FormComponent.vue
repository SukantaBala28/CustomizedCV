<template>
  <div class="container">
    <h1>{{ msg }}</h1>
    <hr/>
    <div class="row text-left">
      <div class="col">
        <form>
          <div class="form-group">
            <label for="firstName">First Name</label>
            <input type="text" name="firstName" class="form-control" id="firstName" placeholder="First Name" v-model="userInfo.firstName" required>
          </div>
          <div class="form-group">
            <label for="lastName">Last Name</label>
            <input type="text" name="lastName" class="form-control" id="lastName" v-model="userInfo.lastName" placeholder="Last Name">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="text" name="email" class="form-control" id="email" v-model="userInfo.email" placeholder="Last Name">
          </div>
        </form>
      </div>
      <div class="col">
        <form>
          <div class="form-group">
            <label for="yourCompany">Company Name</label>
            <input type="text" name="yourCompany" class="form-control" id="yourCompany" v-model="userInfo.companyName" placeholder="First Name">
          </div>
          <div class="form-group">
            <label for="yourAge">Your Age</label>
            <input type="text" name="yourAge" class="form-control" id="yourAge" v-model="userInfo.age" placeholder="Last Name">
          </div>
          <div class="form-group">
            <label for="yourAddress">Your Address</label>
            <input type="text" name="yourAddress" class="form-control" id="yourAddress" v-model="userInfo.address" placeholder="Last Name">
          </div>
          <button type="submit" @click="submitForm" class="btn btn-primary">Submit</button>
        </form>
      </div>
    </div>
    <br/><br/>
    <div class="row">
      <div class="col">
        <button class="btn btn-primary" @click="getInformation">See Your Information</button>
        <h2>Your Information</h2>
        <div>
          <h4>Your First Name: {{getUserInfo.firstName}}</h4>
          <h4>Your Last Name: {{getUserInfo.lastName}}</h4>
          <h4>Your Email: {{getUserInfo.email}}</h4>
          <h4>Your Company Name: {{getUserInfo.companyName}}</h4>
          <h4>Your Age: {{getUserInfo.age}}</h4>
          <h4>Your Address: {{getUserInfo.address}}</h4>
        </div>
      </div>
    </div>
    <br/><br/>
    <button @click="callPdfGenerator()" class="btn btn-primary">Show as PDF</button>
  </div>
</template>

<script>
import Vue from 'vue'
import jsPDF from 'jsPDF'
Vue.use(jsPDF)
export default {
  name: 'FormComponent',
  data () {
    return {
      msg: 'Welcome to Our CV Project App',
      userInfo: {
        firstName: '',
        lastName: '',
        email: '',
        companyName: '',
        age: '',
        address: ''
      },
      getUserInfo: []
    }
  },
  methods: {
    submitForm () {
      localStorage.setItem('UserInfo', JSON.stringify(this.userInfo))
    },
    getInformation () {
      this.getUserInfo = JSON.parse(localStorage.getItem('UserInfo'))
      console.log(this.getUserInfo.lastName)
    },
    callPdfGenerator () {
      var doc = new jsPDF()
      doc.setProperties({
        title: 'This is my title'
      })
      doc.text('Hello world!', 10, 10)
      var string = doc.output('datauristring')
      var iframe = "<iframe width='100%' height='100%' src='" + string + "'></iframe>"
      var x = window.open()
      x.document.open()
      x.document.write(iframe)
      x.document.close()
      // doc.output('dataurlnewwindow')
      // doc.output('save', 'filename.pdf')
      // doc.save('two-by-four.pdf')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
