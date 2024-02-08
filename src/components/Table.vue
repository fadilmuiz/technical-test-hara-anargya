<script>
export default {
  props: ['userList'],
  methods: {
    emitShowPopup(user) {
      this.$emit('showPopup', user);
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return date.toLocaleDateString('en-US', options);
    }
  }
}
</script>

<template>
  <div class="my-5 mx-3 bg-white rounded-xl shadow-lg">
    <div class="border-b-2 border-gray-300">
      <h1 class="py-3 pl-5 text-xl font-medium">User List</h1>
    </div>
    <table class="w-full table-auto rounded-xl">
      <thead class="border-b-2 border-gray-300">
        <tr>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            ID
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            User
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            Date Of Birth
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            Email
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            Job
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            Country
          </th>
          <th scope="col" class="px-2 py-3 text-left text-xs font-medium text-gray-500">
            Action
          </th>
        </tr>
      </thead>
      <tbody class="bg-white divide-y divide-gray-200">
        <tr v-for="user in userList" :key="user.id">
          <td class="px-2 py-2 whitespace-nowrap text-xs">
            <div class="text-sm font-medium text-gray-900">{{ user.id }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-xs flex items-center">
            <img :src="user.profile_picture" class="rounded-full h-8 w-8 object-cover" alt="" />
            <div class="text-sm">{{ user.first_name }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-xs">
            <div class="text-sm text-gray-500">{{ formatDate(user.date_of_birth) }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-xs">
            <div class="text-sm">{{ user.email }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-xs">
            <div class="text-sm text-gray-500">{{ user.job }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-xs">
            <div class="text-sm">{{ user.country }}</div>
          </td>
          <td class="px-2 py-2 whitespace-nowrap text-right text-xs font-medium">
            <button class="border-2 border-gray-300 font-medium py-2 px-4 rounded hover:bg-blue-400">Select</button>
            <button @click="emitShowPopup(user)"
              class="border-2 border-gray-300 font-medium py-2 px-4 rounded ml-2 hover:bg-blue-400">View
              Detail</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


