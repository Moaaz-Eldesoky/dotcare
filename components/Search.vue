<template>
  <form class="search-container">
    <input type="text" id="search-bar" placeholder="Search For Patient (Name, Code, Phone Number)" />
    <nuxt-link class="search_link" to="/">
      <img class="search-icon" src="../static/blue_search_icon.png" />
    </nuxt-link>
  </form>
</template>
<style scoped>
.search-container {
  position: relative;
  margin-top: 10px;
  width: 35rem;
}
#search-bar {
  width: 100%;
  height: 2.5rem;
  /* border: 1px solid #ddd; */
  border:0;
  background-color: #ece9e9;
  border-radius: 5px;
  font-size: 1.12rem;
  padding-left: 1rem;
}
#search-bar:focus {
  border: 0;
}
.search_link{
  position: absolute;
  height: 2.5rem;
  right: 0.5rem;
  top: 0.12rem;
  border-left: 2px solid blue;
  width: 30px;
}
.search-icon{
  position: absolute;
  height: 2rem;
  right: 0.5rem;
  top: 0.25rem;
}

</style>
