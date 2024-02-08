<script>
export default {
  name: 'Popup',
  props: {
    selectedUser: {
      type: Object,
      default: null
    }
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString);
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return date.toLocaleDateString('en-US', options);
    }
  }
};
</script>

<template>
  <transition name="fade-scale" appear>
    <div v-if="selectedUser" class="fixed inset-0 bg-gray-900 bg-opacity-50 flex justify-center items-center">
      <div class="bg-white p-8 rounded-lg flex flex-col relative">
        <div class="flex justify-center items-center mb-4">
          <img :src="selectedUser.profile_picture" class="rounded-full h-24 w-24 object-cover mr-4"
            alt="User's profile picture">
          <div>
            <h2 class="text-2xl font-bold">{{ selectedUser.first_name }} {{ selectedUser.last_name }}</h2>
            <p class="text-lg font-semibold">{{ selectedUser.email }}</p>
            <p class="text-lg font-semibold">{{ selectedUser.phone }}</p>
          </div>
        </div>
        <button @click="$emit('closePopup')"
          class="absolute top-0 right-0 m-4 bg-blue-500 text-white font-bold py-2 px-4 rounded hover:bg-blue-700">Close
        </button>
        <div class="flex justify-center items-center">
          <div>
            <h1>Gender: <span class="text-gray-400 ml-2">{{ selectedUser.gender }}</span></h1>
            <h1>Date Of birth: <span class="text-gray-400 ml-2">{{ formatDate(selectedUser.date_of_birth) }}</span></h1>
            <h1>Street: <span class="text-gray-400 ml-2">{{ selectedUser.street }}</span></h1>
            <h1>City: <span class="text-gray-400 ml-2">{{ selectedUser.city }}</span></h1>
            <h1>Country: <span class="text-gray-400 ml-2">{{ selectedUser.country }}</span></h1>
            <h1>Zipcode: <span class="text-gray-400 ml-2">{{ selectedUser.zipcode }}</span></h1>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<style>
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.3s cubic-bezier(0.55, 0, 0.1, 1);
}

.fade-scale-enter,
.fade-scale-leave-to {
  opacity: 0;
  transform: translateY(50px) scale(0.9);
}

.fade-scale-enter-to,
.fade-scale-leave {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.animate-duration-300 {
  transition-duration: 300ms;
}

.animate-ease-out {
  transition-timing-function: cubic-bezier(0, 0, 0.2, 1);
}

.animate-scale-in {
  animation: scale-in 0.3s cubic-bezier(0.55, 0, 0.1, 1);
}

@keyframes scale-in {
  0% {
    transform: translateY(50px) scale(0.9);
    opacity: 0;
  }

  100% {
    transform: translateY(0) scale(1);
    opacity: 1;
  }
}
</style>


