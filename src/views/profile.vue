<template>
  <div>
    <h1> Add Profile </h1>
      <b-form v-on:submit.prevent="postProfile" @reset="onReset" >
          <b-form-group id="input-group-1" label="Your Name:"  
           label-cols="4" 
           label-cols-lg="2"
           label-for="firstName">
            <b-form-input
              id="firstName"
              v-model="form.firstName"
              required
              placeholder="Enter first name"
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Your Last Name:" label-for="lastName">
            <b-form-input
              id="lastName"
              v-model="form.lastName"
              required
              placeholder="Enter last name"
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Your Date of Birth:" label-for="age">
            <b-form-input id="type-date" type="date" v-model="form.DOB"></b-form-input>
          </b-form-group>

          <b-form-group label="Gender">
            <b-form-radio-group>
              <b-form-radio v-model="gender" name="gender" value="male">Male</b-form-radio>
              <b-form-radio v-model="gender" name="gender" value="female">Female</b-form-radio>
              <b-form-radio v-model="gender" name="gender" value="transgender">TransGender</b-form-radio>
            </b-form-radio-group>
          </b-form-group>

              <div id="address">
                <div v-for="(addr, index) in form.address">
                      <b-form-group id="input-group-2" label="Address Line1:" label-for="lastName">
                        <b-form-input
                          id="lastName"
                          v-model="addr.addressLine1"
                          required
                          placeholder="Enter Address Line1 "
                        ></b-form-input>
                      </b-form-group>
                      <b-form-group id="input-group-2" label="Address Line2:" label-for="lastName">
                        <b-form-input
                          id="lastName"
                          v-model="addr.addressLine2"
                          required
                          placeholder="Enter Address Line 2 "
                        ></b-form-input>
                      </b-form-group>
                       <b-form-group id="input-group-2" label="City :" label-for="lastName">
                        <b-form-input
                          id="lastName"
                          v-model="addr.city"
                          required
                          placeholder="Enter City "
                        ></b-form-input>
                        </b-form-group>
                       <b-form-group id="input-group-2" label="State :" label-for="lastName">
                        <b-form-input
                          id="lastName"
                          v-model="addr.state"
                          required
                          placeholder="Enter State "
                        ></b-form-input>
                        </b-form-group>
                        <b-form-group id="input-group-2" label="Country :" label-for="lastName">
                        <b-form-input
                          id="lastName"
                          v-model="addr.country"
                          required
                          placeholder="Enter country "
                        ></b-form-input>

                      </b-form-group>
                </div>
              </div>  

              <div id="contact">
                      <b-form-group id="input-group-2" label="Phone:" label-for="lastName">
                        <b-form-input
                          id="phone"
                          v-model="form.contact.phones.mobile"
                          required
                          placeholder="Enter Mobile#"
                        ></b-form-input>
                      </b-form-group>
                      <b-form-group id="input-group-2" label="Email:" label-for="lastName">
                        <b-form-input
                          id="Email"
                          v-model="form.contact.emails.personal"
                          required
                          placeholder="Enter Email"
                        ></b-form-input>
                      </b-form-group>
              </div>

          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>

      </b-form>
  </div>
</template>

<script>
import contactaddress from "@/components/contactaddress.vue"
import axios from 'axios'

export default {
   components :{
     contactaddress
   },

    data() {
      return {
        form: {
          firstName: '',
          lastName: '',
          DOB : '',
          gender : 'male',
          age : '',
          address: [],
          contact : {
                   phones : {
                      mobile : '',
                      home : ''
                   },
                   emails : {
                     personal : '',
                     work : ''
                   }
           }
        }
      }
    },
    created: function () {
    // `this` points to the vm instance
    this.addAddress();
    this.addContact();
  },
  computed: {
    age: function () {
      let  years = new Date(new Date() - new Date(this.form.DOB)).getFullYear() - 1970;
      alert(years)
      return years
    }
  },
    methods: {
      postProfile(evt) {
        evt.preventDefault()
              this.form.age = new Date(new Date() - new Date(this.form.DOB)).getFullYear() - 1970;

       alert(JSON.stringify(this.form))
       this.postArtiest(JSON.stringify(this.form))
      },
      addAddress()
      {
        this.form.address.push({addressLine1 : '',addressLine2 : '',city : '',state : '',country : ''})
      },
      addContact()
      {
        this.form.contact.phones.push({mobile : '',home : ''})
        this.form.contact.emails.push({personal : '',work : ''})

      },
      postArtiest(postData)
      {
          let config = {
                          headers: { 'Content-Type': 'application/json' }
                        };

                  axios.post('http://localhost:8080/portfoliomgmt/profile', postData, config).then((response) => {
                                console.log(response.data);
                        });
                    // upload file, get it from this.selectedFile
                  }

      }

    
}
</script>