<template>
  <div id="app">
    <div class="form-group">
      <label for="nama">Nama:</label>
      <input type="text" id="nama" v-model="nama" placeholder="Masukkan nama...">
    </div>
    <div class="form-group">
      <label for="tanggal">Tanggal:</label>
      <input type="date" id="tanggal" v-model="tanggal">
    </div>
    <div class="form-group">
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" placeholder="Masukkan email...">
    </div>

    <h1>Daftar tugas</h1>
    <div class="task-group" v-for="(group, index) in taskGroups" :key="index">
      <h2>{{ group.nama }}</h2>
      <ul v-if="group.tugas.length">
        <li v-for="(tugas, indexTugas) in group.tugas" :key="tugas.id" :class="{ 'selesai': tugas.selesai }">
          <div class="tugas-item">
            <input type="checkbox" :id="'tugas'+tugas.id" v-model="tugas.selesai">
            <label :for="'tugas'+tugas.id" :style="{ color: tugas.warna }">{{ tugas.nama }}</label>
            <span class="tutup-icon" @click="hapusTugas(group, indexTugas)">&times;</span>
          </div>
        </li>
      </ul>
      <p v-else>Tidak ada tugas</p>
      <input type="text" v-model="namaTugasBaru" @keydown.enter="tambahTugas(group)" placeholder="Tambah tugas baru...">
      <button @click="tambahTugas(group)">Tambah Tugas</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      taskGroups: [
        { nama: 'Tugas Kampus', tugas: [] }
      ],
      namaTugasBaru: '',
      nama: '',
      tanggal: '',
      email: ''
    };
  },
  methods: {
    tambahTugas(grup) {
      if (this.namaTugasBaru.trim() !== '') {
        grup.tugas.push({
          id: Date.now(),
          nama: this.namaTugasBaru,
          selesai: false,
          warna: this.pilihWarnaSecaraAcak()
        });
        this.namaTugasBaru = '';
      }
    },
    hapusTugas(grup, index) {
      grup.tugas.splice(index, 1);
    },
    pilihWarnaSecaraAcak() {
      const warna = ['#FF6633', '#FFB399', '#FF33FF', '#FFFF99', '#00B3E6', 
                    '#E6B333', '#3366E6', '#999966', '#99FF99', '#B34D4D',
                    '#80B300', '#809900', '#E6B3B3', '#6680B3', '#66991A', 
                    '#FF99E6', '#CCFF1A', '#FF1A66', '#E6331A', '#33FFCC',
                    '#66994D', '#B366CC', '#4D8000', '#B33300', '#CC80CC', 
                    '#66664D', '#991AFF', '#E666FF', '#4DB3FF', '#1AB399',
                    '#E666B3', '#33991A', '#CC9999', '#B3B31A', '#00E680', 
                    '#4D8066', '#809980', '#E6FF80', '#1AFF33', '#999933', 
                    '#FF3380', '#CCCC00', '#66E64D', '#4D80CC', '#9900B3', 
                    '#E64D66', '#4DB380', '#FF4D4D', '#99E6E6', '#6666FF'];
      return warna[Math.floor(Math.random() * warna.length)];
    }
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  background-color: #5d819c; /* Warna biru muda */
  padding: 20px;
}

h1 {
  text-align: center;
  color: #333;
}

.task-group {
  margin-top: 20px;
  background-color: rgba(221, 212, 212, 0.8); /* Ubah opacity sesuai kebutuhan */
  padding: 20px;
  border-radius: 10px;
}

h2 {
  color: #555;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
}

label {
  margin-left: 5px;
}

.selesai label {
  text-decoration: line-through;
}

input[type="checkbox"] {
  margin-right: 5px;
}

.tugas-item {
  display: flex;
  align-items: center;
}

.tutup-icon {
  margin-left: auto;
  cursor: pointer;
  color: #999;
}

.tutup-icon:hover {
  color: #555;
}

input[type="text"], input[type="date"], input[type="email"], button {
  margin-top: 5px;
}

button {
  background-color: #4CAF50;
  border: none;
  color: rgb(255, 255, 255);
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin-left: 5px;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background-color: #45a049;
}

input[type="text"], input[type="date"], input[type="email"] {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.form-group {
  margin-bottom: 10px;
}

.output {
  margin-bottom: 20px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  background-color: #f9f9f9; /* Warna latar belakang output */
}

.output h2 {
  margin-top: 0;
  color: #333;
}
</style>
