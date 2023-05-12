<script setup lang="ts"></script>

<template>
  <header class="px-20 d-flex flex-row align-items">
    <a href="#" class="d-flex flex-row align-items mr-20">
      <img src="../assets/logo.svg" alt="" />
      <span class="logo">Dyma</span>
    </a>
    <ul class="flex-fill d-flex flex-row">
      <li class="mr-10">
        <a href="">Boutique</a>
      </li>
      <li class="">
        <a href="">Admin</a>
      </li>
    </ul>
    <ul class="d-flex flex-row">
      <li class="mr-10">
        <a href="">Inscription</a>
      </li>
      <li>
        <a href="">Connexion</a>
      </li>
    </ul>
  </header>
</template>

<style lang="scss" scoped>
header{
  background-color: var(--primary-1);
  a{
    color: var(--text-primary-color);
    img{
      width: 20px;
      margin-right: 5px;
    }
    .logo{
      font-weight: 700;
      font-size: 20px;
    }
  }
}
</style>
