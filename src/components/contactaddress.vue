<template>
          <div id="app1">
             <h1> {{form.address.length}} </h1>
            <div v-for="(addr, index) in form.address">
                  <b-form-group id="input-group-2" label="Address Line1:" label-for="lastName">
                    <b-form-input
                      id="lastName"
                      v-model="addr.AddressLine1"
                      required
                      placeholder="Enter Address Line1 "
                    ></b-form-input>
                  </b-form-group>
            </div>
          </div>  
</template>

<script>

</script>
