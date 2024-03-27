<template>
  <header class="flex justify-between border-b border-slate-300 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Sneakers</h2>
        <p class="text-slate-400">The best sneakers store</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <img src="/cart.svg" alt="Cart" />
        <span>$ 120</span>
      </li>
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <img src="/heart.svg" alt="Favorites" />
        <span>Favorites</span>
      </li>
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="Profile" />
        <span>Profile</span>
      </li>
    </ul>
  </header>
</template>
