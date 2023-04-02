<template>
    <nav class="navBar">
        <img class="logo" src="https://www.pngplay.com/wp-content/uploads/10/Rick-And-Morty-Transparent-Images.png" alt="Logo">

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
    background-color:black;
    height: 100px;
    align-items: center;    
  }
  
  .logo{
    margin-left: 2%;
    width: 5%;
  }






  </style>