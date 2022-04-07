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
            <p>Moaaz Eldesoky</p>
          </div>
        </div>
      </div>
    </div>
    <!-- second navbar -->
    <div class="container-fluid">
      <nav class="navbar navbar-expand navbar-light bg-primary routing">
        <div class="nav-menu">
          <b-button
            variant="none"
            class="menu-btn mr-2 ml-0 p-2"
            :class="visible ? null : 'collapsed'"
            :aria-expanded="visible ? 'true' : 'false'"
            aria-controls="collapse-4"
            v-b-modal.modal-1
            @click="visible = !visible"
          >
            <img src="../static/menu_grid_icon.png" class="menu-png-icon mt-n2" />
          </b-button>
          <b-modal
            hide-footer
            hide-header
            id="modal-1"
            class="modal-menu"
            title="product-modal"
          >
            <nuxt-link to="/product">
              <img src="../static/product-icon.jpg" height="30rem" class="ml-5 mt-2"/>
              <p class="menu-product mb-0 ml-4" >Product</p>
            </nuxt-link>
          </b-modal>
        </div>
        <div class="vl-white mr-3"></div>
        <div class="navbar-nav">
          <ul class="navbar-nav">
            <li class="nav-item mt-2">
              <nuxt-link to="/home">
                <img
                  src="../static/house_chimney_icon.png"
                  class="house-png-icon mr-2 pb-1 "
                />
              </nuxt-link>
              <p class="seperator text-white ">></p>
            </li>
            <li class="nav-item">
              <nuxt-link to="/home" class="nav-link text-white ">
                Home
              </nuxt-link>
            </li>
            <li v-if="$nuxt.$route.name != 'home'" class="nav-item">
              <p class="seperator text-white">></p>
              <nuxt-link
                to="product"
                class="nav-link text-white d-inline-block "
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
  height: 30px;
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
    height: 4rem;
overflow: hidden;
}
.menu-product{
  color:#6c6a6a;
  
}

.bg-primary {
  background-color: #0357a8;
}
.menu-png-icon {
  height: 2.5rem;
}
.house-png-icon{
  height: 2.2rem;
}
.seperator {
  display: inline-block;
}
.modal-dialog {
  max-width: 96.1%;
  margin-left: 1.5rem;
  top: 7rem;
  background-color: #baedfa;;
}
.modal-body{
  background: #c8eef9;
  padding: 0px;
}
@media (max-width: 771px) {
  html {
    font-size: 40%;
  }
}
@media (max-width: 540px) {
  html {
    font-size: 34%;
  }
}
</style>
