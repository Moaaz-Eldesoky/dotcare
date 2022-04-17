<template>
  <div>
    <h1>welcome...</h1>
    <p>filtered array : {{filtration}}</p>
  </div>
</template>
<script>
export default {
  data: () =>{
    arr:[{name:"moaaz",job:"teacher"},{name:"marwan",jop:"eng"}]
  },
  computed:{
    filtration(){
      let filtered_arr= this.arr.filter(el=>el.name=="moaaz")
      return filtered_arr;
    }
  }
}
</script>
