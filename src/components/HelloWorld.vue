<template>
  <div class="hello">
   <b-row>
     <b-col>
        <b-card no-body class="overflow-hidden" style="max-width: 540px;">
          <b-row>
            <b-col md="6">
              <b-card-img src="https://picsum.photos/400/400/?image=20" class="rounded-0"></b-card-img>
            </b-col>
            <b-col md="6">
              <b-card-body title="Personal Details">
                <b-card-text align="left">
                    First Name : {{posts.firstName}}  <br>
                    Last Name  : {{posts.lastName}}  <br>
                    Age        : {{posts.age}} <br>
                    Gender     : {{posts.gender}}
                </b-card-text>
              </b-card-body>  
            </b-col>              
          </b-row>
      </b-card>
     </b-col>   
   </b-row>      
   <b-row>
     <b-col>
        <div>
          <b-card no-body>
            <b-tabs card v-model="tabIndex" align="ceter" >
              <b-tab title="Address" :title-link-class="linkClass(0)">
             <li v-for="addr in posts.address">
                Address Line1 : {{addr.addressLine1}}  <br>
                Address Line2 : {{addr.addressLine2}}  <br>
                City          : {{addr.city}} <br>
                State         : {{addr.state}} <br>
                Postal Code   : {{addr.postalCode}} <br>
              </li>  
              </b-tab>
              <b-tab title="Skills" :title-link-class="linkClass(1)">
                <li v-for="skill in posts.skills">
                    Skill Name : {{skill.skillname}}  <br>
                    Experience : {{skill.expinMonths}} (Months)<br>  
                </li>  
              </b-tab>
              <b-tab title="Phone" :title-link-class="linkClass(2)">
                Mobile Phone  : {{posts.contact.phones.mobile}}  <br>
                Home Phone    : {{posts.contact.phones.home}}   <br>
                Work Phone    : {{posts.contact.phones.work}}
              </b-tab>
              <b-tab title="Email" :title-link-class="linkClass(3)">
                Email 1 : {{posts.contact.emails.personal}}  <br>
                Email 2 : {{posts.contact.emails.work}} <br>
              </b-tab>
            </b-tabs>
          </b-card>
        </div>
        </b-col>
    </b-row> 
        <b-row>
        <b-col>
                    <b-card header="Social Medial Links" class="text-center">
                          <b-card-text> 
                            facebook   :  <br>
                            Instagram  :  <br>
                          </b-card-text>
                    </b-card>
        </b-col>
    </b-row>  
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HelloWorld',
  props: 
    {
      category : String
    },
  data() {
    return {
      posts: [],
      errors: [],        
      tabIndex: 0

    }
  },
  getName:  function () 
  {
     return this.posts.firstName + " " + this.posts.lastName;
  },
  methods: 
  {
      linkClass(idx) 
      {
        if (this.tabIndex === idx) 
        {
          return ['bg-primary', 'text-light']
        } else 
        {
          return ['bg-light', 'text-info']
        }
      }
  },
  // Fetches posts when the component is created.
  async created() {
   try {
       const response = await axios.get('http://localhost:8080/portfoliomgmt/profile/5c965da6ed8773555265c8e0')
       this.posts = response.data
       }  
   catch (e) 
       {
         this.errors.push(e)
       }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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