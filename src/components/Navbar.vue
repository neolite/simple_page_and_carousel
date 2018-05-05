<template>
  <nav class="navbar is-fixed-top is-primary" role="navigation" aria-label="main navigation">

  <div class="navbar-brand">
    <div class="navbar-burger burger" :class="{ 'is-active': selected }" data-target="navMenu" @click="selected=!selected">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>

    <div class="navbar-menu" id="navMenu" :class="{ 'is-active': selected }" >
      <div class="navbar-start">
          <router-link class="navbar-item" @click.native="selected=false" to="/" exact>Home</router-link>
          <router-link class="navbar-item" @click.native="selected=false" to="/about">About us</router-link>
          <router-link class="navbar-item" @click.native="selected=false" to="/contact">Contact us</router-link>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  name: "Navbar",
  data() {
    return {
      selected: false
    };
  }
};
</script>
