<template>
  <div class="app">
    <h1>𝓐𝓰𝓮𝓷𝓭𝓪 𝓡𝓪𝓶𝓪𝓭𝓱𝓪𝓷</h1>
    <input v-model="kegiatanBaru" @keyup.enter="tambahKegiatan" placeholder="Tambahkan kegiatan (Enter)" />
    <ul>
      <li v-for="(kegiatan, index) in kegiatanList" :key="index" v-show="kegiatan.tampil !== false">
        <input type="checkbox" v-model="kegiatan.selesai" @change="ubahStatusKegiatan(index)">
        <span :class="{ 'selesai': kegiatan.selesai }" :style="{'text-decoration': kegiatan.selesai ? 'line-through' : 'none'}">{{ kegiatan.nama }}</span>
        <button @click="ubahStatusKegiatan(index)">
          {{ kegiatan.selesai ? 'Belum Selesai' : 'Selesai' }}
        </button>
        <button @click="hapusKegiatan(index)">Batal</button>
      </li>
    </ul>
    <button @click="tampilkanBelumSelesai">Filter Belum Selesai</button>
    <button @click="tampilkanSemua">Tampilkan Semua</button>
  </div>
</template>


<script>
export default {
  data() {
    return {
      kegiatanBaru: '',
      kegiatanList: [
        { nama: 'Sahur', selesai: true, tampil: true },
        { nama: 'Mengaji', selesai: false, tampil: true },
        { nama: 'Sholat', selesai: false, tampil: true },
      ],
    };
  },
  methods: {
    tambahKegiatan() {
      if (this.kegiatanBaru !== '') {
        this.kegiatanList.push({ nama: this.kegiatanBaru, selesai: false, tampil: true });
        this.kegiatanBaru = '';
      }
    },
    hapusKegiatan(index) {
      this.kegiatanList.splice(index, 1);
    },
    ubahStatusKegiatan(index) {
      this.kegiatanList[index].selesai = !this.kegiatanList[index].selesai;
    },
    tampilkanBelumSelesai() {
      this.kegiatanList.forEach((kegiatan) => {
        kegiatan.tampil = !kegiatan.selesai;
      });
    },
    tampilkanSemua() {
      this.kegiatanList.forEach((kegiatan) => (kegiatan.tampil = true));
    },
  },
};
</script>
