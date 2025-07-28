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
          <td><router-link to="/words">📘 Word Table</router-link></td>
          <td>View and manage your vocabulary words.</td>
        </tr>
        <tr>
          <td><router-link to="/words/new">🆕 Add New Word</router-link></td>
          <td>Add a new word to the database.</td>
        </tr>
        <tr>
          <td><router-link to="/test">📝 Test Yourself</router-link></td>
          <td>Try a quiz to check your vocabulary!</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'user'
};
</script>
