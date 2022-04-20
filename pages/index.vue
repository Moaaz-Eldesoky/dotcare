<template>
  <section class="home-page">
    <div class="content text-center">
      <img src="../static/main-logo-2.png" class="main-logo" height="200rem" alt="Main logo" />
      <p>Welcome...</p>
    </div>
  </section>
</template>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

<script>
export default {
  head(){
      return {
          title:"dotcare project created with vue js",
          meta:[{
              hid:'description',
              name:'description',
              content:'this project only for testing my skills to have a place in Alandalosia-company internship',
          }]
        }
    }
}
</script>

<style>
body{
  background-color: #eff7ff;
}
.home-page{
    height: 40rem;
    background-color: #eefbff;
    clip-path: circle(95.1% at 50% 210%);
}
.content{
  /* padding-top: 5rem; */
    margin-top: 6rem;
}
.content img{
  margin-bottom: 2rem;
}
</style>
