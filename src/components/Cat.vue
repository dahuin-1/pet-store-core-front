<template>
  
   <Pet v-model="value">

       <template v-slot:buttons>
       <v-btn outlined="outlined" 
                rounded="rounded" 
                text="text" 
                 @click="groom">groom</v-btn>
       </template>

   </Pet>
  
</template>

<script>

  const axios = require('axios').default;

   import Pet from './Pet'

   export default {
     name: 'Cat',

     mixins: [Pet],

     components:{
        Pet
     },

     methods:{

       async groom(){
           
         await axios.request({
              method: 'PUT',
              url: new URL(this.value._links.groom.href).pathname,
              headers: {'Content-Type': 'application/json'}
        });

        this.refresh();

        },

       }
    }
</script>