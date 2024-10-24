
<template >
  <div class="out">
  <form novalidate class="md-layout" @submit.prevent="handleSubmit">
    <md-card class="md-layout-item md-size-50 md-small-size-100 bg-grey rounded">
      <md-card-content> 
      <md-field>
        <label>Name</label>
        <md-input v-model="postData.name"></md-input>
      </md-field>
  
      <md-field>
        <label>Description</label>
        <md-input v-model="postData.description"></md-input>
      </md-field>
  
      <md-button type="submit" v-on:click="submitData()" class="md-raised md-primary" >Submit</md-button>
         </md-card-content>
    </md-card></form>
  </div>
  </template>
  <style>
  .out{
        min-height: 100vh;  
        background-size:     cover;
    /* background-image: url("https://drmcet.ac.in/wp-content/uploads/2022/05/slider1.jpg");  */
  }
    
    .md-card{
      margin-top: 8%;
      margin-left: 25%;
      
  }
  </style>
  <script>
    
  export default {
    name: 'FormValidation',
    data: () => ({
      postData: {
        name: '',
        description: '', 
      }
     
    }),
    methods: {
      handleSubmit() {
  if (!this.postData.name || !this.postData.description) {
    alert('Please fill in all fields.');
    return;
  }
  
  this.submitData().then(() => {
    this.$router.go();
  });
},
     
       submitData() {
      const apiUrl = 'http://127.0.0.1:8000/api/';
      const options = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.postData)
      };

      fetch(apiUrl, options)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          console.log('Data received:', data);
     
        })
        .catch(error => {
          console.error('There was a problem with the fetch operation:', error);
         
        });
    },
    },

  }
  
</script>
  
     