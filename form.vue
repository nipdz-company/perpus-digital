<template>
  <div class="container-fluid">
    <div class="row justify-content-center text-white">
      <div class="col-lg-7">
        <h1 class="text-center">Form insert</h1>
        <div class="card">
          <div class="card-header bg-dark">
            <h3>Isi Kunjungan</h3>
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
              <div v-if="kategori === 'Siswa' " class="form-group-py3">
                <label for="exampleFormControlSelect1">kelas</label>
                <select v-model="kelas" class="form-control-form-select" id="exampleFormControlSelect1">
                <option value="X PPLG 1">X PPLG 1</option>
                <option value="X PPLG 2">X PPLG 2</option>
                <option value="X PPLG 3">X PPLG 3</option>
                <option value="X PPLG 4">X PPLG 4</option>
                <option value="XI PPLG 1">XI PPLG 1</option>
                <option value="XI PPLG 2">XI PPLG 2</option>
                <option value="XI PPLG 3">XI PPLG 3</option>
                <option value="XI PPLG 4">XI PPLG 4</option>
                </select>
              </div>
              <!-- <div class="mb-3">
                <input v-model="kelas" type="text" class="form-control" placeholder="KELAS..." required>
              </div> -->
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
  <div class="button-action text-end">
    <NuxtLink class="btn btn-light rolunded-pil " to="/">back</NuxtLink>
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
  @import url('https://fonts.googleapis.com/css2?family=Handlee&family=Indie+Flower&family=Josefin+Sans:wght@400;500&family=Lato&family=Libre+Baskerville&display=swap');



.btn:hover {
  transform: scale(0.95);
  transition: all .2s ease-in-out;
}


.btn-light {
  border-radius: 17px;
  background: #D9D9D9;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  width: 80px;
  height: 40px;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-top: 70px;
  margin-right: 22%;
  font-family: 'Josefin Sans', sans-serif;

}

/* h3 { 
  font-family: 'Lato', sans-serif;

} */


</style>