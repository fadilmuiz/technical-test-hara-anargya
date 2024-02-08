<script>
import axios from 'axios';
import SideBar from '../components/SideBar.vue'
import Card from '../components/Card.vue'
import UserTable from '../components/Table.vue'
import UserPopup from '../components/PopUp.vue'

export default {
  name: 'HomeView',
  components: {
    SideBar,
    Card,
    UserTable,
    UserPopup
  },
  data() {
    return {
      userList: [],
      selectedUser: null
    };
  },
  created() {
    this.fetchUserList()
  },
  methods: {
    async fetchUserList() {
      try {
        const response = await axios.get('https://api.slingacademy.com/v1/sample-data/users');
        this.userList = response.data.users;
      } catch (error) {
        console.error('Error fetching user list:', error);
      }
    },
    showPopup(user) {
      this.selectedUser = user;
    },
    closePopup() {
      this.selectedUser = null;
    }
  }
}
</script>

<template>
  <div class="flex bg-gray-200">
    <SideBar :isDashboardPage="true" :isOverviewPage="false"/>
    <div class="max-w-screen overflow-x-hidden">
      <div class="bg-white w-screen h-14 shadow-lg">
        <h1 class="text-lg font-bold py-3 pl-7 ">Conversion</h1>
      </div>
      <div class="flex my-6">
        <Card/>
      </div>
      <UserTable :userList="userList" @showPopup="showPopup" />
    </div>
    <UserPopup :selectedUser="selectedUser" @closePopup="closePopup" />
  </div>
</template>
