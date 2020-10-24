<script lang="ts">
  import {
    slide,
  } from 'svelte/transition';

  let isOpen = false;

  let links = [{
      name: "Home",
      link: "/"
    },
    {
      name: "About",
      link: "/about"
    },
    {
      name: "Contact",
      link: "/contact"
    }
  ];
</script>

<header class="dark-bg sm:flex sm:justify-between sm:items-center sm:px-4 sm:py-3">
  <div class="flex items-center px-4 py-4 justify-between sm:p-0">
    <div>
      <img class="h-6" src="img/logo.svg" alt="Zack Myers Blog">
    </div>
    <div class="sm:hidden">
      <button on:click={()=> isOpen = !isOpen} type="button" class="block text-gray-500 hover:text-white
        focus:text-white focus:outline-none">
        {#if isOpen == false}
        <svg class="h-6 w-6 fill-current" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
          stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        {:else}
        <svg class="h-6 w-6 fill-current" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
          stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
        {/if}
      </button>
    </div>
  </div>
  {#if isOpen == true}
  <div class="px-2 pt-2 pb-4 sm:block">
    {#each links as link}
      <a transition:slide class="mt-1 block px-2 py-1 text-white font-semibold rounded transition-all duration-150 hover:bg-gray-800" href={link.link}>{link.name}</a>
    {/each}
  </div>
  {/if}
  <div class="p-0 hidden sm:flex">
    {#each links as link}
      <a transition:slide class="ml-2 block px-2 py-1 text-white font-semibold rounded transition-all duration-150 hover:bg-gray-800" href={link.link}>{link.name}</a>
    {/each}
  </div>
</header> 

<style>
  a {
    font-family: 'Inter'
  }

  .dark-bg {
    background-color: #0B0B0B;
  }
</style>