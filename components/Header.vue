<template>
  <header class="header">
    <!-- white navbar -->
    <div class="container-fluid p-1 m-0 acount-and-lang bg-white mb-2">
      <div class="d-flex justify-content-between">
        <div class="logo"><nuxt-link to="/"><img src="../static/Logo.png" /></nuxt-link></div>
        <div class="d-flex justify-content-around">
          <div class="lang-droupdown-button">
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
          <nuxt-link
            to="/profile"
            class="account d-flex justify-content-center m-auto"
            style="text-decoration: none"
          >
            <img class="user-img" src="../static/user-icon.png" />
            <p>Moaaz Eldesoky</p>
          </nuxt-link>
        </div>
      </div>
    </div>
    <!-- blue navbar -->
    <div class="container-fluid">
      <nav class="navbar navbar-expand navbar-light bg-primary routing">
        <div class="nav-menu">
          <b-button
            variant="none"
            class="menu-btn mr-2 ml-0 p-2"
            id="show-btn"
            @click="
              !visible
                ? ($bvModal.show('modal-1'), (visible = !visible))
                : ($bvModal.hide('modal-1'), (visible = !visible))
            "
            v-model="visible"
          >
            <img
              src="../static/menu_grid_icon.png"
              class="menu-png-icon mt-n2"
            />
          </b-button>
          <div class="container">
            <b-modal id="modal-1" class="modal-menu" hide-footer hide-header>
              <nuxt-link
                to="/product"
                class="product-link"
                style="text-decoration: none"
              >
                <div
                  class="click-effect-hide"
                  @click="$bvModal.hide('modal-1')"
                >
                  <img
                    src="../static/product-icon.jpg"
                    height="30rem"
                    class="modal-img ml-5 mt-2"
                  />
                  <p class="menu-product mb-0 ml-4">Product</p>
                </div>
              </nuxt-link>
            </b-modal>
          </div>
        </div>
        <div class="vl-white mr-3"></div>
        <div class="navbar-nav">
          <ul class="navbar-nav">
            <li class="nav-item mt-2">
              <nuxt-link to="/">
                <img
                  src="../static/house_chimney_icon.png"
                  class="house-png-icon mr-2 pb-1"
                />
              </nuxt-link>
              <p class="seperator text-white">></p>
            </li>
            <li class="nav-item">
              <nuxt-link to="/" class="nav-link text-white"> Home </nuxt-link>
            </li>
            <li v-if="$nuxt.$route.name != 'index'" class="nav-item">
              <p class="seperator text-white">></p>
              <nuxt-link
                to="product"
                class="nav-link text-white d-inline-block"
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
.logo img {
  height: 2.5rem;
  margin-top: 1rem;
  margin-left: 1rem;
}
.user-img {
  height: 3rem;
  margin-top: 0.5rem;
}
.account p {
  font-size: 1.25rem;
  word-spacing: -0.2rem;
  padding-top: 1rem;
  margin-left: 1rem;
  margin-right: 1rem;
}
.vl {
  border-left: 1px solid #ddd;
  height: 30px;
}
.vl-white {
  border-left: 2px solid white;
  height: 30px;
}
.lang-droupdown-button {
  padding-top: 0.5rem;
  z-index: 99999;
}
.lang-droupdown-button .btn {
  padding-top: 0.5rem;
  font-size: 1.5rem;
  color: blue;
}

.routing {
  font-size: 1.25rem;
  height: 4rem;
  overflow: hidden;
  z-index: 1070;
}

.menu-product {
  color: #6c6a6a;
}
.modal-img {
  height: 3rem;
}
.product-link p {
  color: #0357a8;
}
.bg-primary {
  background-color: #0357a8;
}
.menu-png-icon {
  height: 2.5rem;
}
.house-png-icon {
  height: 2.2rem;
}
.seperator {
  display: inline-block;
}
.modal-dialog {
  max-width: 100%;
  margin-left: 1.5rem;
  margin-right: 3.25rem;
  top: 8rem;
  background-color: #baedfa;
}
.modal-body {
  background: #c8eef9;
  padding: 0px;
}
@media (max-width: 771px) {
  html {
    font-size: 40%;
  }
  .modal-dialog {
    margin-right: 5rem;
    margin-left: 2.25rem;
    top: 8.5rem;
  }
}
@media (max-width: 540px) {
  html {
    font-size: 34%;
  }
  .modal-dialog {
    margin-right: 5.75rem;
    margin-left: 2.75rem;
    top: 10.5rem;
  }
}
</style>
