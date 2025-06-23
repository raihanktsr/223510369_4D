<script setup>
import { ref, computed } from 'vue'

// --- DATA ---
// 1. Declarative Rendering: Data ini akan kita tampilkan di template.
const eventName = ref('Ngoding Bareng: Belajar Vue.js dari Dasar');
const eventDescription = ref('Sebuah acara untuk belajar konsep dasar Vue.js secara interaktif.');

// 4. Form Bindings: Variabel untuk menyimpan nilai dari input form.
const name = ref('');
const email = ref('');

// 5. Conditional Rendering: State untuk menentukan apakah pendaftaran sudah berhasil.
const isRegistered = ref(false);


// --- LOGIC / COMPUTED ---
// 2. Attribute Bindings: Menghitung apakah form sudah lengkap atau belum.
// Hasilnya (true/false) akan digunakan untuk menonaktifkan tombol.
const isFormIncomplete = computed(() => {
  return name.value === '' || email.value === '';
});


// --- METHODS ---
// 3. Event Listeners: Fungsi ini akan dijalankan saat form di-submit.
function handleSubmit() {
  if (!isFormIncomplete.value) {
    // Di aplikasi nyata, di sini kita akan mengirim data ke server.
    // Untuk studi kasus ini, kita hanya akan mengubah state.
    console.log('Pendaftaran berhasil:', { name: name.value, email: email.value });
    isRegistered.value = true;
  }
}
</script>

<template>
  <div class="container">
    <header>
      <h1>{{ eventName }}</h1>
      <p>{{ eventDescription }}</p>
    </header>

    <main>
      <form v-if="!isRegistered" @submit.prevent="handleSubmit" class="registration-form">
        <h2>Formulir Pendaftaran</h2>
        
        <div class="form-group">
          <label for="name">Nama Lengkap:</label>
          <input type="text" id="name" v-model="name" placeholder="Masukkan nama Anda">
        </div>
        
        <div class="form-group">
          <label for="email">Alamat Email:</label>
          <input type="email" id="email" v-model="email" placeholder="Masukkan email Anda">
        </div>

        <button type="submit" :disabled="isFormIncomplete">
          Daftar Sekarang
        </button>
      </form>

      <div v-else class="confirmation">
        <h2>Terima Kasih!</h2>
        <p>Pendaftaran Anda atas nama <strong>{{ name }}</strong> telah kami terima.</p>
        <p>Detail lebih lanjut akan kami kirimkan ke email <strong>{{ email }}</strong>.</p>
      </div>
    </main>
  </div>
</template>

<style scoped>
/* Ini adalah styling agar tampilan lebih rapi, tidak wajib untuk fungsionalitas */
.container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

header {
  text-align: center;
  border-bottom: 1px solid #ddd;
  padding-bottom: 20px;
  margin-bottom: 20px;
}

h1 {
  color: #2c3e50;
}

h2 {
  color: #34495e;
}

.registration-form, .confirmation {
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box; /* Penting agar padding tidak menambah lebar */
}

button {
  width: 100%;
  padding: 12px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #3aa875;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.confirmation {
  text-align: center;
}
</style>