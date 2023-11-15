<template>
  <div class="container-fluid bg-img">
    <div class="row justify-content-end">
      <div class="col-lg-5">
        <h1 class="text-center">Form insert</h1>
        <div class="card">
          <div class="card-header bg-dark text-white">
            <h3>ISI KUNJUNGAN</h3>
          </div>
          <div class="card-body">
            <div v-if="terkirim" class="alert alert-success">Berhasil tercatat di buku kunjungan!</div>
            <div v-if="gagal" class="alert alert-danger">Terjadi kesalahan!</div>
            
            <form @submit.prevent="kirim()">
              <div class="mb-3">
                <input v-model="nama" type="text" class="form-control" placeholder="NAMA..." required>
              </div>
              <div class="mb-3">
                <select v-model="kategori" class="form-control">
                  <option value="">PILIH KATEGORI ANGGOTA</option>
                  <option value="Siswa">Siswa</option>
                  <option value="Guru">Guru</option>
                  <option value="Staff">Staff</option>
                  <option value="Umum">Umum</option>
                </select>
              </div>
              <div class="mb-3">
                <input v-model="kelas" type="text" class="form-control" placeholder="KELAS..." required>
              </div>
              <div class="mb-3">
                <textarea v-model="keperluan" class="form-control" cols="30" rows="3" placeholder="KEPERLUANNYA APA...."
                  required></textarea>
              </div>
              <button type="submit" class="btn btn-dark rounded-pill">Kirim</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const nama = ref('')
const kelas = ref('')
const keperluan = ref('')
const kategori = ref('')
const supabase = useSupabaseClient()
const terkirim = ref(false)
const gagal = ref(false)

async function kirim() {
  const { error } = await supabase
    .from('formulir')
    .insert([
      {
        kategori: kategori.value,
        nama: nama.value,
        kelas: kelas.value,
        keperluan: keperluan.value,
      }
    ])
  if (error) gagal.value = true
  else terkirim.value = true
}


async function bacaData() {
  const { data, error } = await supabase.from('formulir').select()
  if (data) console.log(data)
}

onMounted(() => bacaData())
</script>

<style scoped>
.card {
  
}
.btn:hover {
  transform: scale(0.95);
  transition: all .2s ease-in-out;
}

.bg-img {
  width: 100%;
  height: 100%;
  background: transparent url ("@/assets/img/form.png") no-repeat center center fixed;
  background-size: cover;
  }
</style>