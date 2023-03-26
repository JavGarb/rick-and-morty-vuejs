<template>
    <nav class="navBar">
        <img class="logo" src="https://www.pngplay.com/wp-content/uploads/10/Rick-And-Morty-Transparent-Images.png" alt="Logo">
        <div class="links">
            <a href="#">About me</a>
            <button @click="showFavorites">Favoritos</button>
        </div>
      <p  class="search">
        Busqueda
        <input type="text">
        <button>Search</button>
      </p>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'NavBar'
  }
  </script>
  
  <style>
  /* Estilos para el navBar */
  .navBar{
    margin: 0%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    background-color: bisque;
    height: 100px;
    align-items: center;    
  }
  
  .logo{
    margin-left: 2%;
    width: 5%;
  }

  .search{
    margin-right: 2%;
  }

  .links a{
    margin-left: 50px;

  }

  .search input{
    height: 25px;
    margin: 10px;
    color: azure;
    background-color:darkblue;
  }
  </style>