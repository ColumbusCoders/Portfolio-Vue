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
              <br>
              <br>
              <ul v-if="results && results.length">
              <h6> Result(s) :  {{results.length}}   </h6>                
                      <div>
                            <b-table small :fields="tabfields" :items="results">
                                <!-- A virtual column -->
                                <template slot="index" slot-scope="data">
                                  {{ data.index + 1 }}
                                </template>

                                <!-- A custom formatted column -->
                                <template slot="name" slot-scope="data">
                                  {{ data.item.firstName }} {{ data.item.lastName }}
                                </template>

                                <!-- A virtual composite column -->
                                <template slot="addr" slot-scope="data">
                                    {{data.value.addressLine1}}<br>
                                    {{data.value.addressLine2}}<br>
                                    {{data.value.city}},{{data.value.state}}
                                </template>
                            </b-table>                      
                       </div>  
              </ul>             
  </div>
</template>

<script>
import axios from 'axios'

  export default {
    data() {
      return {
        tabfields: [
          // A virtual column that doesn't exist in items
          'index',
          // A column that needs custom formatting
          { key: 'name', label: 'Full Name' },
          // A regular column
          'age',
          // A regular column
          'gender',
          // A virtual column made up from two fields
          { key: 'addr', 
            label: 'Address',
            formatter: (value, key, item) => {
              let str = JSON.parse(JSON.stringify(item.address[0]))
              return str
            }
          }
        ],
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
       // alert(JSON.stringify(this.form))
 axios.get('http://localhost:8080/portfoliomgmt/profile?firstName=' + this.form.firstName)
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