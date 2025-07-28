<template>
  <div>
    <h1>Nguyen Bao Minh Week 12 - Words</h1>

    
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search words"
      class="ui input fluid"
      style="margin-bottom: 1rem;"
    />

    
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

      <tbody>
        <tr v-for="(word, i) in filteredWords" :key="i">
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
      </tbody>
    </table>
  </div>
</template>

<script>
import { api } from '../helpers/helpers';

export default {
  name: 'words',
  data() {
    return {
      words: [],
      searchQuery: ''
    };
  },
  computed: {
    filteredWords() {
      const query = this.searchQuery.trim().toLowerCase();
      if (!query) return this.words;

   
      return this.words.filter(word => {
        const values = Object.values(word).map(v => String(v).toLowerCase());
        return values.some(val => val.includes(query));
      });
    }
  },
  methods: {
    async onDestroy(id) {
      const sure = window.confirm('Are you sure?');
      if (!sure) return;

      await api.deleteWord(id);
      this.flash('Word deleted successfully!', 'success');
      this.words = this.words.filter(word => word._id !== id);
    }
  },
  async mounted() {
    this.words = await api.getWords();
  }
};
</script>

<style scoped>
input[type="text"] {
  padding: 0.6rem;
  font-size: 1rem;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
