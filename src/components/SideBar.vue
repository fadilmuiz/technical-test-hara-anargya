<script>
export default {
  name: 'SideBar',
  props: {
    isDashboardPage: Boolean,
    isOverviewPage: Boolean
  }
}
</script>

<template>
  <div :class="{ 'bg-blue-200': isDashboardPage, 'bg-blue-200': isOverviewPage }" class="flex bg-white">
    <aside class="w-52 bg-white border-r border-gray-200">
      <div class="pt-8 pl-6">
        <h1 @click.prevent="$router.push('/')" class="text-lg text-4xl font-extrabold">heylink.</h1>
      </div>
      <div class="pt-8 pl-6 pr-2">
        <ul class="space-y-2 text-sm font-normal">
          <li @click.prevent="$router.push('/')" :class="{ 'rounded-md bg-blue-400': isDashboardPage }" class="flex items-center hover:bg-blue-400 rounded-md pl-1">
            <img src="../assets/dash.png" alt="Dashboard Icon" class="w-6 h-6 mr-2">
            <a href="#"
              class="block text-black-600 pl-1 py-2">Dashboard</a>
          </li>
          <li @click.prevent="$router.push('/over-view')"  :class="{ 'rounded-md bg-blue-400': isOverviewPage }" class="flex items-center hover:bg-blue-400 rounded-md pl-1 ">
            <img src="../assets/over.png" alt="Overview Icon" class="w-6 h-6 mr-2">
            <a href="#"
              class="block text-black-600 pl-1 py-2 rounded-md ">Overview</a>
          </li>
        </ul>
      </div>

    </aside>
  </div>
</template>