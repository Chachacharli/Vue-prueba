<template>
    <nav class="flex items-center justify-between flex-wrap bg-[#202124] border-b-[1px] border-gray-300 p-6">
  <div class="flex items-center flex-shrink-0 text-white mr-6">
    <i class="bi bi-check2-square mx-2 text-xl"></i>
    <span class="font-semibold text-xl tracking-tight">Todo app Scisa</span>
  </div>
  <div class="block lg:hidden">
    <button class="flex items-center px-3 py-2 border rounded text-purple-50 border-teal-400 hover:text-white hover:border-white">
      <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
    </button>
  </div>

</nav>
</template>

<script>
export default{
    name: "Nav"
}
</script>