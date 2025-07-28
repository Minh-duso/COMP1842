<template>
  <div id="app">
    <div class="ui inverted segment navbar">
      <div class="ui center aligned container">
        <div class="ui large secondary inverted pointing menu compact ">

          <router-link to="/words" exact class="item">
            <i class="comment outline icon" style="color:blue;"></i> Words
          </router-link>

          <router-link to="/words/new" class="item">
            <i class="plus circle icon" style="color:greenyellow;"></i> New
          </router-link>

          <router-link to="/test" class="item">
            <i class="graduation cap icon" style="color:red;"></i> Test
          </router-link> 

          <router-link to="/user" class="item">
            <i class="user secret icon" style="color:brown;"></i> Minh Profile
          </router-link>
        </div>
      </div>
    </div>

    <div class="ui text container">
    <flash-message class="myFlash"></flash-message>
      <div class="ui one column grid">
        <div class="column">
          <router-view />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app'
};
</script>

<style>


#app > div.navbar {
  margin-bottom: 1.5em;
  background-color: seagreen ;
}
.myFlash {
  width: 250px;
  margin: 10px;
  position: absolute;
  top: 50;
  right: 0;
}
input {
  width: 300px;
}
div.label {
  width: 120px;
}
div.input {
  margin-bottom: 10px;
}
button.ui.button {
  margin-top: 15px;
  display: block;
}

#app {
  min-height: 100vh;
  background-image: url('@/assets/liem.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  color: white
}


</style>