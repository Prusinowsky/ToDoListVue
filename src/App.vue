<template>
  <div id="app">
    <div>
      <b-navbar toggleable="lg" type="dark" variant="primary">
        <b-container>
          <b-navbar-brand href="#">To Do List</b-navbar-brand>
          <b-collapse  is-nav>
            <b-navbar-nav class="ml-auto">
              <b-nav-item to="/" exact exact-active-class="active">Home</b-nav-item>
              <b-nav-item to="about" exact-active-class="active">About</b-nav-item>
            </b-navbar-nav>
          </b-collapse>
        </b-container>
      </b-navbar>
    </div>
    <b-container class="mt-5 text-left" >
      <router-view></router-view>
    </b-container>
  </div>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Nunito+Sans&display=swap");

  #app {
    font-family: Nunito Sans, system-ui, BlinkMacSystemFont, -apple-system, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  #nav {
    padding: 30px;
    a {
      font-weight: bold;
    color: #2c3e50;

      &.active {
      color: #fff;
      }
    }
  }
</style>
