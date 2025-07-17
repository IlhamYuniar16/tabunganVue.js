<template>
  <div class="dark:bg-gray-700 transition-all duration-300 dark:shadow-lg shadow-lg">
    <section class="flex justify-between container m-auto p-5 items-center">
        <div>
          <div class="flex gap-5 items-center">
            <h1 class="dark:text-white text-2xl font-bold">Tabungan: {{ usernameMe }}</h1>
            <svg @click="editUser" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 dark:text-white ">
              <path stroke-linecap="round" stroke-linejoin="round" d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L6.832 19.82a4.5 4.5 0 0 1-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 0 1 1.13-1.897L16.863 4.487Zm0 0L19.5 7.125" />
          </svg>
          </div>
          <div v-if="openUser" class="relative">
            <form action="" @submit.prevent="submitUser" class="flex flex-col items-start">
              <input v-model="usernameMe" type="text" placeholder="Masukan Username Anda" class="pr-10 pl-3 py-1 border focus:ring-1 focus:outline-none focus:ring-blue-400 border-blue-400 rounded-2xl">
              <button type="submit" class="bg-blue-400 px-23 rounded-2xl mt-3 py-2 text-white hover:bg-blue-500 transition  cursor-pointer">Pasang</button>
            </form>
          </div>
        </div>
        <button @click="darkMode" class="bg-white rounded-full p-1 shadow-lg dark:bg-gray-700 transition-all duration-300">
          <div v-if="dark">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 text-white">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 3v2.25m6.364.386-1.591 1.591M21 12h-2.25m-.386 6.364-1.591-1.591M12 18.75V21m-4.773-4.227-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z" /></svg>
          </div>
          <div v-else>
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 dark:text-white">
              <path stroke-linecap="round" stroke-linejoin="round" d="M21.752 15.002A9.72 9.72 0 0 1 18 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 0 0 3 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 0 0 9.002-5.998Z" /></svg>
          </div>
        </button>
    </section>
  </div>
  <div class="dark:bg-gray-700 min-h-screen transition-all duration-300 lg:pt-10">
    <div class="dark:bg-gray-800 dark:text-white max-w-3xl mx-auto p-6 transition-all duration-300 rounded-2xl shadow-lg space-y-8">
      <h1 class="text-3xl font-bold text-center text-blue-800">Pencatatan Tabungan & Pengeluaran</h1>

      <!-- Nabung -->
      <section>
        <h2 class="text-xl font-semibold text-blue-700 mb-2">Nabung</h2>
        <form @submit.prevent="saveTabungan" class="space-y-4">
          <input type="number" v-model="nabung" placeholder="Masukkan jumlah tabungan"
            class="w-full px-4 py-2 rounded-lg border border-blue-300 focus:outline-none focus:ring-2 focus:ring-blue-400" />
          <div class="flex gap-4">
            <button type="submit"
              class="flex-1 bg-blue-600 text-white py-2 rounded-lg hover:drop-shadow transition drop-shadow-xl/60 drop-shadow-blue-500 hover:drop-shadow-blue-500 cursor-pointer">Nabung</button>
            <button type="button" @click="resetTabungan"
              class="flex-1 bg-orange-500 text-white py-2 rounded-lg hover:bg-orange-500 hover:drop-shadow transition drop-shadow-xl/60 drop-shadow-orange-500 hover:drop-shadow-orange-500 cursor-pointer">Reset Tabungan</button>
          </div>
        </form>
      </section>

      <!-- Pengeluaran -->
      <section>
        <h2 class="text-xl font-semibold text-blue-700 mb-2">Pengeluaran</h2>
        <form @submit.prevent="saveData" class="space-y-4">
          <input type="text" v-model="category" placeholder="Kategori"
            class="w-full px-4 py-2 rounded-lg border border-blue-300 focus:outline-none focus:ring-2 focus:ring-blue-400" />
          <input type="number" v-model="quantity" placeholder="Jumlah"
            class="w-full px-4 py-2 rounded-lg border border-blue-300 focus:outline-none focus:ring-2 focus:ring-blue-400" />
          <input type="number" v-model="price" placeholder="Harga"
            class="w-full px-4 py-2 rounded-lg border border-blue-300 focus:outline-none focus:ring-2 focus:ring-blue-400" />
          <input type="date" v-model="tanggal" placeholder="Harga"
            class="w-full px-4 py-2 rounded-lg border border-blue-300 focus:outline-none focus:ring-2 focus:ring-blue-400" />
          <div class="flex gap-4">
            <button type="submit"
              class="flex-1 bg-blue-600 text-white py-2 rounded-lg hover:drop-shadow transition drop-shadow-xl/60 drop-shadow-blue-500 hover:drop-shadow-blue-500 cursor-pointer">Simpan</button>
            <button type="button" @click="resetPengeluaran"
              class="flex-1 bg-orange-500 text-white py-2 rounded-lg hover:bg-orange-500 hover:drop-shadow transition drop-shadow-xl/60 drop-shadow-orange-500 hover:drop-shadow-orange-500 cursor-pointer">Reset Pengeluaran</button>
          </div>
        </form>
      </section>

      <!-- Tabel -->
      <section>
        <h2 class="text-xl font-semibold text-blue-700 mb-4">Daftar Pengeluaran</h2>
        <div class="overflow-x-auto">
          <table class="min-w-full table-auto border border-blue-200">
            <thead class="bg-blue-100 text-blue-800">
              <tr>
                <th class="px-4 py-2 border">No</th>
                <th class="px-4 py-2 border">Kategori</th>
                <th class="px-4 py-2 border">Jumlah</th>
                <th class="px-4 py-2 border">Harga</th>
                <th class="px-4 py-2 border">Tanggal</th>
                <th class="px-4 py-2 border">Aksi</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in data" :key="index" class="text-center">
                <td class="px-4 py-2 border">{{ index + 1 }}</td>
                <td class="px-4 py-2 border">{{ item.category }}</td>
                <td class="px-4 py-2 border">{{ item.quantity }}</td>
                <td class="px-4 py-2 border">Rp {{ item.price }}</td>
                <td class="px-4 py-2 border">{{ item.tanggal }}</td>
                <td class="px-4 py-2 border">
                  <button @click="hapus(index)"
                    class="bg-red-500 hover:bg-red-600 cursor-pointer text-white px-4 py-1 rounded-md transition"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" /></svg>
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>

      <!-- Total -->
      <section class="text-center">
        <h2 class="text-xl font-semibold text-blue-700">Sisa Tabungan</h2>
        <p class="text-3xl font-bold text-green-600 mt-2">Rp {{ total }}</p>
      </section>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted, computed } from 'vue'

const category = ref('')
const quantity = ref(0)
const price = ref(0)
const tanggal = ref('')
const nabung = ref(0)
const data = ref([])
const tabungan = ref(0)
const dark = ref(false)
const usernameMe = ref('')
const openUser = ref(false)


function darkMode() {
  dark.value = !dark.value
  const data = document.documentElement.classList.contains('dark')
  if(data) {
      localStorage.theme = "light"
      document.documentElement.classList.remove('dark')
  } else {
      localStorage.theme = "dark"
      document.documentElement.classList.add('dark')
    }
  }


onMounted(() => {
  if(localStorage.theme === 'dark') {
    document.documentElement.classList.add('dark')
    dark.value = true
  } else {
    document.documentElement.classList.remove('dark')
    dark.value = false
  }
})


function editUser() {
  openUser.value = !openUser.value
}

function submitUser() {
  const name = usernameMe.value.trim()
  if (!name) return

  localStorage.setItem('usernameMe', name)
  openUser.value = false
}

function saveTabungan() {
  if (!nabung.value || nabung.value <= 0) return
  tabungan.value += Number(nabung.value)
  localStorage.setItem('DataTabungan', JSON.stringify(tabungan.value))
  nabung.value = 0
}

function saveData() {
  if (!category.value || quantity.value <= 0 || price.value <= 0 || tanggal.value === '') return
  data.value.push({ category: category.value, quantity: Number(quantity.value), price: Number(price.value), tanggal: tanggal.value })
  localStorage.setItem('DataMe', JSON.stringify(data.value))
  category.value = ''
  quantity.value = 0
  price.value = 0
}

function hapus(index) {
  data.value.splice(index, 1)
  localStorage.setItem('DataMe', JSON.stringify(data.value))
}

function resetPengeluaran() {
  data.value = []
  localStorage.removeItem('DataMe')
}

function resetTabungan() {
  tabungan.value = 0
  localStorage.removeItem('DataTabungan')
}

function getData() {
  const saved = localStorage.getItem('DataMe')
  if (saved) data.value = JSON.parse(saved)
}

function getTabungan() {
  const saved = localStorage.getItem('DataTabungan')
  if (saved) tabungan.value = JSON.parse(saved)
}

function getUser() {
  const saved = localStorage.getItem('usernameMe')
  if (saved) {
    usernameMe.value = saved
    openUser.value = false
  } else {
    openUser.value = true
  }
}

const total = computed(() => {
  const pengeluaran = data.value.reduce((sum, item) => sum + item.price * item.quantity, 0)
  return tabungan.value - pengeluaran
})

onMounted(() => {
  getData()
  getTabungan()
  getUser()
})
</script>
