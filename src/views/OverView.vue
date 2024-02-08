<script>
import SideBar from '../components/SideBar.vue';
import cities from '../city';
import provinces from '../province';

export default {
  name: 'OverView',
  components: {
    SideBar,
  },
  data() {
    return {
      provinces: provinces,
      cities: cities,
      selectedSortOrder: 'asc',
      order: 'asc',
      cityId: '',
      provinceId: '',
      provinceName: null,
      citiesByProvince: []
    };
  },
  methods: {
    getCities() {
      this.citiesByProvince = this.getCitiesByProvinceId(this.provinceId);
    },
    getProvinceName() {
      this.provinceName = this.getProvinceNameByCityId(parseInt(this.cityId));
    },
    getCitiesByProvinceId(provinceId) {
      return this.cities.filter(city => city.provinceId === parseInt(provinceId));
    },
    getProvinceNameByCityId(cityId) {
      const city = this.cities.find(city => city.id === cityId);
      if (city) {
        const province = this.provinces.find(province => province.id === city.provinceId);
        if (province) {
          return province;
        }
      }
      return null;
    },
    sortProvincesById(order) {
      if (order === 'asc') {
        this.provinces.sort((a, b) => a.id - b.id);
      } else if (order === 'desc') {
        this.provinces.sort((a, b) => b.id - a.id);
      }
    },
    sortProvincesByName(order) {
      if (order === 'asc') {
        this.provinces.sort((a, b) => a.name.localeCompare(b.name));
      } else if (order === 'desc') {
        this.provinces.sort((a, b) => b.name.localeCompare(a.name));
      }
    },
  },
  computed: {
    sortedProvinces() {
      return [...this.provinces];
    }
  }
}
</script>

<template>
  <div class="flex bg-gray-100">
    <SideBar :isDashboardPage="false" :isOverviewPage="true" />
    <div class="max-w-screen overflow-x-hidden">
      <div class="bg-white w-screen h-14 shadow-lg">
        <h1 class="text-lg font-bold py-3 pl-7 ">Conversion</h1>
      </div>
      <!-- card -->
      <div class="container mx-auto mt-8">
        <!-- Dropdown filter By ID -->
        <label for="sortOrderId" class="mr-2 ml-5">Sort By Id:</label>
        <select v-model="selectedSortOrder" id="sortOrderId"
          class="border rounded-md px-3 py-2 focus:outline-none focus:border-blue-500">
          <option value="asc">A-Z</option>
          <option value="desc">Z-A</option>
        </select>
        <button @click="sortProvincesById(selectedSortOrder)"
          class="bg-blue-500 text-white px-4 py-2 rounded-md ml-2 hover:bg-blue-600 focus:outline-none focus:bg-blue-600">Terapkan</button>
        <!-- Dropdown filter By Name -->
        <label for="sortOrderName" class="mr-2 ml-5">Sort By Name:</label>
        <select v-model="order" id="sortOrderName" class="border rounded-md px-3 py-2 focus:outline-none focus:border-blue-500">
          <option value="asc">A-Z</option>
          <option value="desc">Z-A</option>
        </select>
        <button @click="sortProvincesByName(order)"
          class="bg-blue-500 text-white px-4 py-2 rounded-md ml-2 hover:bg-blue-600 focus:outline-none focus:bg-blue-600">Terapkan</button>
        <!-- Daftar provinsi -->
        <div class="bg-white-500 ml-3">
          <div class="container mx-auto mt-5">
            <div class="grid grid-cols-3 gap-4">
              <div v-for="province in sortedProvinces" :key="province.id"
                class="max-w-xs rounded-xl overflow-hidden shadow-xl">
                <div class="px-6 py-4">
                  <img :src="province.img" class="rounded h-52 w-80 object-cover mt-2" alt="" />
                  <div class="flex justify-center items-center mb-4">
                    <p class="font-bold text-xl my-2 mr-2">{{ province.name }}</p>
                    <p class="font-bold text-xl mb-2">{{ province.id }}</p>
                  </div>
                  <p class="font-medium text-lg text-gray-500">{{ province.msg }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Fitur pencarian kota berdasarkan id provinsi  -->
      <div class="container mx-auto max-w-md p-4 mt-8">
        <div class="bg-white-500 ml-3 mt-8 h-72">
          <h2 class="text-lg font-bold mb-2">Daftar Kota Berdasarkan ID Provinsi</h2>
          <div class="flex items-center">
            <input type="text" v-model="provinceId"
              class="flex-1 border rounded-md px-3 py-2 mr-2 focus:outline-none focus:border-blue-500"
              placeholder="Masukkan ID Provinsi">
            <button @click="getCities"
              class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600">Cari</button>
          </div>
          <div v-if="citiesByProvince.length > 0" class="bg-gray-100 rounded-md p-4 mt-4">
            <p class="text-lg font-semibold mb-2">Daftar Kota:</p>
            <ul>
              <li v-for="city in citiesByProvince" :key="city.id" class="mb-1">{{ city.name }}</li>
            </ul>
          </div>
          <p v-else class="text-red-500 mt-2">Tidak ada kota yang ditemukan untuk provinsi dengan ID tersebut.</p>
        </div>
        <!-- Fitur pencarian berdasarkan nama provinsi berdasarkan id kota -->
        <div class="container mx-auto max-w-md p-4 mt-8 h-96">
          <h2 class="text-lg font-bold mb-2">Cari Nama Provinsi Berdasarkan ID Kota</h2>
          <div class="flex items-center">
            <input type="text" v-model="cityId"
              class="flex-1 border rounded-md px-3 py-2 mr-2 focus:outline-none focus:border-blue-500"
              placeholder="Masukkan ID Kota">
            <button @click="getProvinceName"
              class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600">Cari</button>
          </div>

          <div v-if="provinceName !== null" class="bg-white-500 mt-1">
            <div class="container ">
              <div class="rounded-xl overflow-hidden shadow-xl">
                <div class="px-6 py-4">
                  <img :src="provinceName.img" class="rounded h-44 w-96 object-cover" alt="" />
                  <div class="flex justify-center items-center mb-4">
                    <p class="font-bold text-xl my-2 mr-2">{{ provinceName.name }}</p>
                    <p class="font-bold text-xl mb-2">{{ provinceName.id }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <p v-else class="text-red-500 mt-2">Tidak ada Provinsi yang ditemukan untuk Kota dengan ID tersebut.</p>
        </div>
      </div>
    </div>
  </div>
</template>
