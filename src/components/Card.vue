<script>
export default {
  name: 'Card'
};
</script>

<template>
  <!-- card 1 -->
  <div class="bg-white rounded-lg shadow-lg w-80 mx-3">
    <div class="flex justify-between items-center mb-4 px-4 py-2 relative">
      <div>
        <h2 class="text-lg font-medium text-gray-500">Pending</h2>
        <h3 class="text-xl font-medium text-gray-800">2.480,<span class="text-gray-500">30</span></h3>
      </div>
      <img src="../assets/Group 6.png" alt="Logo" class="logo absolute top-2 right-2">
    </div>
    <div class="px-4 pb-4">
      <div class="flex justify-between">
        <div class="flex text-sm">
          <p class="text-green-500">2,15%</p>
          <p class="text-gray-400 ml-2">Last Month</p>
        </div>
        <div class="w-1/2 pl-2 text-sm">
          <p class="text-gray-500 font-bold pl-14">View More</p>
        </div>
      </div>
    </div>
  </div>
  <!-- card 2 -->
  <div class="bg-white rounded-lg shadow-lg w-80 mx-3">
    <div class="flex justify-between items-center mb-4 px-4 py-2 relative">
      <div>
        <h2 class="text-lg font-medium text-gray-500">Paid</h2>
        <h3 class="text-xl font-medium text-gray-800">84.310</h3>
      </div>
      <img src="../assets/Group 6.png" alt="Logo" class="logo absolute top-2 right-2">
    </div>
    <div class="px-4 pb-4">
      <div class="flex justify-between">
        <div class="flex text-sm">
          <!-- <img src="../assets/right-down.png" alt="Logo" class="w-3 h-3"> -->
          <p class="text-red-500">1,10%</p>
          <p class="text-gray-400 ml-2">Last Month</p>
        </div>
        <div class="w-1/2 pl-2 text-sm">
          <p class="text-gray-500 font-bold pl-14">View More</p>
        </div>
      </div>
    </div>
  </div>
  <!-- card 3 -->
  <div class="bg-white rounded-lg shadow-lg w-80 mx-3">
    <div class="flex justify-between items-center mb-4 px-4 py-2 relative">
      <div>
        <h2 class="text-lg font-medium text-gray-500">Rejected</h2>
        <h3 class="text-xl font-medium text-gray-800">12.155</h3>
      </div>
      <img src="../assets/Group 6.png" alt="Logo" class="logo absolute top-2 right-2">
    </div>
    <div class="px-4 pb-4">
      <div class="flex justify-between">
        <div class="flex text-sm">
          <p class="text-green-500">2,15%</p>
          <p class="text-gray-400 ml-2">Last Month</p>
        </div>
        <div class="w-1/2 pl-2 text-sm">
          <p class="text-gray-500 font-bold pl-14">View More</p>
        </div>
      </div>
    </div>
  </div>
</template>