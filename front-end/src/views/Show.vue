<template>
  <div>
    <h1>Show Word</h1>

    <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="germany flag"></i> German
      </div>
      <input type="text" readonly :value="word.german" />
    </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="united kingdom flag"></i> English
      </div>
      <input type="text" readonly :value="word.english" />
    </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="vietnam flag"></i> Vietnamese
    </div>
    <input type="text" readonly :value="word.vietnamese" />
    </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
       <i class="thailand flag"></i> Thai
    </div>
   <input type="text" readonly :value="word.thai" />
    </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
       <i class="philippines flag"></i> Filipino
    </div>
   <input type="text" readonly :value="word.filipino" />
    </div>


  </div>
</template>

  
  <script>
  import { api } from '../helpers/helpers';

  export default {
    name: 'show',
    data() {
      return {
        word: ''
      };
    },
    async mounted() {
      this.word = await api.getWord(this.$route.params.id);
    }
  };
  </script>
  
  