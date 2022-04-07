<template>
  <section class="home-page">
    <div class="content text-center">
      <img src="../static/main-logo.png" height="300px" alt="Main logo" />
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
  background-color: #fff;
}
.home-page{
    height: 40rem;
    background-color: #ecfbff;
    clip-path: circle(81.1% at 50% 177%);
}
.content{
    margin-top: 6rem;
}
</style>