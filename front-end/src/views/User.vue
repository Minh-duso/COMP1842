<template>
  <div>
    <h1>Minh Profile</h1>
    <p>This is my web Site. Please read the description to understand how it work</p>

    <h2>📂 My Page</h2>
    <table class="ui celled table">
      <thead>
        <tr>
          <th>Feature</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <a href="#" @click.prevent="goToPage('/words')">📘 Word Table</a>
          </td>
          <td>View and manage your vocabulary words.</td>
        </tr>
        <tr>
          <td>
            <a href="#" @click.prevent="goToPage('/words/new')">🆕 Add New Word</a>
          </td>
          <td>Add a new word to the database.</td>
        </tr>
        <tr>
          <td>
            <a href="#" @click.prevent="goToPage('/test')">📝 Test Yourself</a>
          </td>
          <td>Try a quiz to check your vocabulary!</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'user',
  methods: {
    goToPage(path) {
      this.$router.push({ path, query: { from: 'profile' } });
    }
  }
};
</script>
