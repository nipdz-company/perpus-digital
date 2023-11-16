<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-lg-8">
        <h1 class="text-center">Visitors</h1>
        <div class="card">
          <div class="card-header bg-dark text-white">
            <h3>RIWAYAT PENGUNJUNG</h3>
          </div>
          <div class="card-body">
            <table class="table table-striped">
              <thead>
                <tr class="table-dark">
                  <th class="text-center">No</th>
                  <th class="text-center">Kategori</th>
                  <th class="text-center">Nama</th>
                  <th class="text-center">Kelas</th>
                  <th class="text-center">Tanggal</th>
                  <th class="keperluan text-center">Keperluan</th>
                </tr>
              </thead>
              <tbody v-for="(formulir, visitors) in datas" :key="formulir.id" class="tablepengunjung ">

                <td class="text-center">{{ visitors + 1 }}</td>


                <td class="text-center">{{ formulir.kategori }}</td>


                <td class="text-center">{{ formulir.nama }}</td>


                <td class="text-center">{{ formulir.kelas }}</td>


                <td class="text-center">{{ formulir.date }}</td>

                <td class="text-center">{{ formulir.keperluan }}</td>

              </tbody>
            </table>
            <div class="button-action text-end">
              <NuxtLink class="btn btn-dark rolunded-pil " to="/">back</NuxtLink>
            </div>
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
const tanggal = ref('')
const kategori = ref('')
const supabase = useSupabaseClient()
const datas = ref([])
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
        date: tanggal.value,
        keperluan: keperluan.value,
      }
    ])
  if (error) gagal.value = true
  else terkirim.value = true
}


async function bacaData() {
  const { data, error } = await supabase.from('formulir').select()
  if (data)
    console.log(data)
  datas.value = data
}

onMounted(() => bacaData())
</script>

<style scoped>
/* .text-center {
  color: white;
} */

.container-fluid {
  background-color: #28353D;
}

.btn:hover {
  transform: scale(0.95);
  transition: all .2s ease-in-out;
}

.btn-dark {
  border-radius: 17px;
  background: #D9D9D9;
  width: 80px;
  height: 40px;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-top: 70px;
  margin-right: 5%;
  font-family: 'Josefin Sans', sans-serif;
}

table {
  border: #000;
}

/* .table-striped>tbody>tr:nth-child(odd)>th {
   background-color: red; 
 } */
</style>