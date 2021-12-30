<template>
  
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <a class="navbar-brand" href="#">SGP</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="collapsibleNavbar">
    <ul class="navbar-nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/cidades">Cidades</router-link>
    </ul>
  </div>  
</nav>

<div class="container" style="margin-top:30px">
  <div class="row">
    
    <div class="col-sm-12">
        <router-view/>

    </div>
  </div>
</div>

<div class="jumbotron text-center" style="margin-bottom:0">
  <p>Desenvolvido por : Alan Tavares</p>
</div>




</template>

<style>

</style>
