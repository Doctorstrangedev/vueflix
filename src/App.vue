<template>
 
 <nav class="navbar navbar-light p-0">
      <div class="container-fluid px-5">
        <router-link class="navbar-brand" to="/">Vueflix</router-link>
      </div>
</nav>
<main>
<router-view/>
</main>


  
</template>

<style lang="scss">

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Nunito Sans', sans-serif;
  overflow-x:hidden ;
}

body{
  background-color: #000000;
}
.navbar {
   position: absolute !important;
   width: 100%;
}

a.navbar-brand {
   color: #e50914 !important;
   font-size: 44px;
   font-weight: bold;
}
</style>
