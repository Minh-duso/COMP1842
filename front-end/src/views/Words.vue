<template>
  <div>
     <h1>Nguyen Bao Minh Week 12- Words</h1>
     <table id="words" class="ui celled compact table">
     <thead>
       <tr>
       <th>English</th>
       <th>German</th>
       <th>Vietnamese</th>
       <th>Thai</th>
       <th>Filipino</th>
       <th colspan="3"></th>
       </tr>
     </thead>
     <tr v-for="(word, i) in words" :key="i">
  <td>{{ word.english }}</td>
  <td>{{ word.german }}</td>
  <td>{{ word.vietnamese }}</td>
  <td>{{ word.thai }}</td>
  <td>{{ word.filipino }}</td>
  
  <td width="75" class="center aligned">
    <router-link :to="{ name: 'show', params: { id: word._id } }">Show</router-link>
  </td>

  <td width="75" class="center aligned">
    <router-link :to="{ name: 'edit', params: { id: word._id } }">Edit</router-link>
  </td>

  <td width="75" class="center aligned">
  <a href="#" @click.prevent="onDestroy(word._id)">Destroy</a>
  </td>
        </tr>
     </table>
    </div>
</template>

<script>
import { api } from '../helpers/helpers';

export default {
    name: 'words',
    data() {
        return {
            words: []
        };
    },
    methods: {
      async onDestroy(id) {
        const sure = window.confirm('Are you sure?');
        if (!sure ) return;
        console.log("Deleting word with ID:", id);
        await api.deleteWord(id);
        this.flash('Word deleted successfully!', 'success');
        const newWords = this.words.filter(word => word._id !== id);
        this.words = newWords;
      }
    },
    async mounted() {
        this.words = await api.getWords();
         console.log("Loaded words:", this.words);
    }
};
</script>