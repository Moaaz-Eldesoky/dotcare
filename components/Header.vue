<template>
  <header class="header">
    <!-- first navbar -->
    <div class="container-fluid p-1 m-0 acount-and-lang bg-white mb-2">
      <div class="d-flex justify-content-between">
        <div class="logo"><img src="../static/Logo.png" height="20" /></div>
        <div class="account d-flex justify-content-around">
          <div class="droupdown-button">
            <b-dropdown
              variant="outline-none"
              id="dropdown-1"
              text="English"
              class="mr-3"
            >
              <b-dropdown-item>Arabic</b-dropdown-item>
              <b-dropdown-item>French</b-dropdown-item>
              <b-dropdown-item>Germany</b-dropdown-item>
            </b-dropdown>
          </div>
          <div class="vl mr-3"></div>
          <div class="account d-flex justify-content-center m-auto">
            <img src="../static/user-icon.png" height="30" />
            <p>sabry elsayed farag mahmoud</p>
          </div>
        </div>
      </div>
    </div>
    <!-- second navbar -->
    <div class="container-fluid routing">
      <nav class="navbar navbar-expand navbar-light bg-primary">
        <div class="nav-menu-btn">
          <b-button
            variant="primary"
            class="mr-2 ml-0"
            :class="visible ? null : 'collapsed'"
            :aria-expanded="visible ? 'true' : 'false'"
            aria-controls="collapse-4"
            @click="visible = !visible"
          >
            <img src="../static/menu_grid_icon.png" class="png-icon mt-n2" />
          </b-button>
          <b-collapse id="collapse-4" v-model="visible" class="mt-2">
            <b-card-group deck class="card-group" >
              <nuxt-link to="/product">    <!--style="width: 100rem-->
                <b-card
                  img-src="../static/product-icon.jpg"
                  img-alt="Card image"
                  img-top
                >
                  <b-card-text> Product </b-card-text>
                </b-card>
              </nuxt-link>
            </b-card-group>
          </b-collapse>
        </div>
        <div class="vl-white mr-3"></div>
        <div class="navbar-nav">
          <ul class="navbar-nav">
            <li class="nav-item m-auto pr-2">
              <nuxt-link to="/home">
                <img
                  src="../static/house_chimney_icon.png"
                  class="png-icon mr-2 mt-n2"
                />
              </nuxt-link>
              <p class="seperator text-white m-auto">></p>
            </li>
            <li class="nav-item">
              <nuxt-link to="/home" class="nav-link text-white mt-1">
                Home
              </nuxt-link>
            </li>
            <li v-if="$nuxt.$route.name != 'home'" class="nav-item">
              <p class="seperator text-white">></p>
              <nuxt-link
                to="product"
                class="nav-link text-white d-inline-block mt-1"
              >
                {{ $nuxt.$route.name }}
              </nuxt-link>
            </li>
          </ul>
        </div>
      </nav>
    </div>
  </header>
</template>
<script>
export default {
  name: "Header",
  data() {
    return {
      visible: false,
    };
  },
};
</script>

<style>
html {
  font-size: 62.5%;
}
body {
  font-family: "lato", sans-serif;
  font-size: 1.6rem;
  line-height: 1.7;
  box-sizing: border-box;
    background-color: #d8e9fa;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}
.nav-menu-btn {
  height: 20px;
}
.vl {
  border-left: 1px solid #ddd;
  height: 30px;
}
.vl-white {
  border-left: 2px solid white;
  height: 30px;
}
.droupdown-button .btn {
  padding: 0;
  font-size: 1.5rem;
}
.account p {
  font-size: 1.25rem;
  word-spacing: -0.2rem;
}
.routing {
  font-size: 1.25rem;
}
.card-group {
  max-width: 100%;
}
.card-group img {
  width: 2.7rem;
  margin-left: 2rem;
}
.card-body {
  padding-top: 5px;
}
.bg-primary {
  background-color: #0357a8;
}
.png-icon {
  height: 2.2rem;
}
.seperator {
  display: inline-block;
}
@media (max-width:771px) {
    html {
  font-size: 38%;
}
}
@media (max-width:540px) {
    html {
  font-size: 34%;
}
}
</style>
