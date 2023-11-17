<template>
  <div class="container-fluid">
    <div class="row justify-content-center text-white">
      <div class="col-lg-7">
        <h1 class="text-center">Form insert</h1>
        <div class="card">
          <div class="card-header bg-dark">
            <h3>Insert here</h3>
          </div>
          <div class="card-body">
            <div v-if="terkirim" class="alert alert-success">Berhasil tercatat di buku kunjungan!</div>
            <div v-if="gagal" class="alert alert-danger">Terjadi kesalahan!</div>

            <form @submit.prevent="kirim()">
              <div class="mb-3">
                <input v-model="nama" type="text" class="form-control" placeholder="Nama" required>
              </div>
              <div class="mb-3">
                <p style="color: black;">Kategori</p>
                <select v-model="kategori" class="form-control" placeholder="Kategori" required>
                  <option value="Siswa">Siswa</option>
                  <option value="Guru">Guru</option>
                  <option value="Staff">Staff</option>
                  <option value="Umum">Umum</option>
                </select>
              </div>
              <div v-if="kategori === 'Siswa'" class="form-group-py3 text-dark">KELAS
                <div class="kls">
                  <select v-model="kelas" class="form-control-form-select" id="exampleFormControlSelect1">
                    <option value="X">X</option>
                    <option value="XI">XI</option>
                    <option value="XII">XII</option>
                  </select>
                  <select v-model="jurusan" class="form-control-form-select" id="exampleFormControlSelect1">
                    <option value="TJKT">TJKT</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TSM">TSM</option>
                    <option value="DKV">DKV</option>
                    <option value="TOI">TOI</option>
                  </select>
                  <select v-model="nokelas" class="form-control-form-select" id="exampleFormControlSelect1">
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                  </select>
                </div>
              </div>
              <div class="mb-3 py-3">
                <textarea v-model="keperluan" class="form-control" cols="30" rows="3" placeholder="Keperluan"
                  required></textarea>
              </div>
              <button type="submit" class="btn btn-dark rounded-pill">Submit</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
  <NuxtLink class="btn btn-light1 rolunded-pil " to="/">back</NuxtLink>
  <NuxtLink class="btn btn-light2 rounded-pil" to="/visitors">See</NuxtLink>
  <div class="button-action text-end">
  </div>
</template>

<script setup>
const nama = ref('')
const kelas = ref('')
const keperluan = ref('')
const kategori = ref('')
const nokelas = ref('')
const jurusan = ref('')
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
        jurusan: jurusan.value,
        nokelas: nokelas.value,
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
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;500&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Handlee&family=Josefin+Sans:wght@400;500&display=swap');


.btn:hover {
  transform: scale(0.95);
  transition: all .2s ease-in-out;
}

.card-body {
  font-family: 'Josefin Sans', sans-serif;
}

.btn-light1 {
  border-radius: 17px;
  background: #D9D9D9;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  width: 80px;
  height: 40px;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-top: 30px;
  font-family: 'Josefin Sans', sans-serif;
  position: relative;
  left: 62%;
}



.btn-light2 {
  border-radius: 17px;
  background: #D9D9D9;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  width: 80px;
  height: 40px;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-top: 30px;
  font-family: 'Josefin Sans', sans-serif;
  position: relative;
  left: 65%;
}



.form-control-form-select {
  border-radius: 5px;
  border: 1px solid lightgray;
}

.kls {
  display: grid;
  grid-template-columns: 33% 33% 33%;
  border-radius: 7px;
  background-color: white;
  border: 1px solid lightgray;
  padding: 10px;
}

.form-control ::placeholder {
  color: #000;
}

.form-control-form-select option {
  text-align: center;
}

/* h3 { 
  font-family: 'Lato', sans-serif;

} */
</style>