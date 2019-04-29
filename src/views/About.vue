<template>
  <div>
    <b-form v-on:submit.prevent="getResults" @reset="onReset" v-if="show">

      <b-form-group id="exampleInputGroup2" label="Search by Name:" label-for="exampleInput2">
        <b-form-input
          id="firstName"
          type="text"
          v-model="form.firstName"
          required
          placeholder="Enter Name" />
      </b-form-group>
    

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
                 <li v-for="result in results">
                    <b-card-group deck>
                      <b-card header="Default" class="text-center">
                          <b-card-text> 
                            First Name : {{result.firstName}}  <br>
                            Last Name  : {{result.lastName}} <br>
                            Age        : {{result.age}} <br>
                            Gender     : {{result.gender}} <br>
                          </b-card-text>
                      </b-card>
                   </b-card-group>
                 </li>  
  </div>
</template>

<script>
import axios from 'axios'

  export default {
    data() {
      return {
      results : [],
      errors: [],  
        form: {
          firstName: '',
          age : ''
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true
      }
    },
    methods: {
      getResults(evt) {
        evt.preventDefault()
        alert(JSON.stringify(this.form))
 axios.get('http://localhost:8080/artiest/name/' + this.form.firstName)
    .then(response => {
      // JSON responses are automatically parsed.
      this.results = response.data
      alert(results.length)
    })
    .catch(e => {
      this.errors.push(e)
    })
       alert(results.length)
      },
      onReset(evt) {
        evt.preventDefault()
        /* Reset our form values */
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        /* Trick to reset/clear native browser form validation state */
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>