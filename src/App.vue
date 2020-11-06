<template>
  <div id="app">
     <Login></Login>
  </div>
</template>

<script>
     import Login from "@/views/Login";
     export default {
       components: {Login}
     }

</script>

<style>

    html,body{
      width: 100%;
      height: 100%;
      margin: 0;
    }

    body {
      background-color: #F2F6FC;
    }

  #app{
    width: 100%;
    height: 100%;
  }
</style>
