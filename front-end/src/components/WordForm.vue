<template>
  <form action="#" @submit.prevent="onSubmit">
     <p v-if="errorsPresent" class="error">Please fill out both fields!</p>
 
     <div class="ui labeled input fluid">
       <div class="ui label">
         <i class="germany flag"></i> German
       </div>
       <input type="text" placeholder="Enter word..." v-model="word.german" />
     </div>
 
     <div class="ui labeled input fluid">
       <div class="ui label">
         <i class="united kingdom flag"></i> English
       </div>
       <input type="text" placeholder="Enter word..." v-model="word.english" />
     </div>

     <div class="ui labeled input fluid">
       <div class="ui label">
        <i class="vietnam flag"></i> Vietnamese
      </div>
      <input type="text" placeholder="Enter word..." v-model="word.vietnamese" />
     </div>
     
     <div class="ui labeled input fluid">
       <div class="ui label">
        <i class="thailand flag"></i> Thai
     </div>
     <input type="text" placeholder="Enter Thai..." v-model="word.thai" />
     </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
      <i class="philippines flag"></i> Filipino
    </div>
    <input type="text" placeholder="Enter Filipino..." v-model="word.filipino" />
     </div>

 
     <button class="positive ui button">Submit</button>
   </form>
 </template>
 
 <script>
 export default {
   name: 'word-form',
   props: {
     word: {
       type: Object,
       required: false,
       default: () => {
        return {
          english: '',
          german: '',
          vietnamese: '',
          thai: '',
          filipino: ''
        };
       }
     }
   },
   data() {
     return {
       errorsPresent: false
     };
   },
   methods: {
    onSubmit: function() {
  if (this.word.english === '' || this.word.german === '') {
    this.errorsPresent = true;
  } else {
    this.errorsPresent = false;
    this.$emit('createOrUpdate', this.word);
  }
}

   }
 };
 </script>
 