<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-lg-20">
        <h1 class="text-center text-white">Visitors</h1>
        <div class="card">
          <div class="card-header bg-dark text-white">
            <h3>Visit History</h3>
          </div>
          <div class="card-body">
            <div> total pengunjung : {{ datas.length }} </div>
            <table class="table rounded-pil">
              <thead>
                <tr class="table-dark">
                  <th class="text-center">No</th>
                  <th class="text-center">Kategori</th>
                  <th class="text-center">Nama</th>
                  <th class="text-center">Kelas</th>
                  <th class="text-center">Tanggal</th>
                  <th class="text-center">Keperluan</th>
                  <th class="text-center">jurusan</th>
                  <th class="text-center">Rombel</th>
                </tr>
              </thead>
              <tbody v-for="(formulir, visitors) in datas" :key="formulir.id" class="tablepengunjung ">

                <td class="text-center">{{ visitors + 1 }}</td>


                <td class="text-center">{{ formulir.kategori }}</td>


                <td class="text-center">{{ formulir.nama }}</td>


                <td class="text-center">{{ formulir.kelas }}</td>


                <td class="text-center">{{ formulir.date }}</td>


                <td class="text-center">{{ formulir.keperluan }}</td>


                <td class="text-center">{{ formulir.jurusan }}</td>


                <td class="text-center">{{ formulir.nokelas }}</td>


              </tbody>
            </table>
          </div>
        </div>
        <div class="kls text-end">
          <NuxtLink class="btn btn-dark rolunded-pil" to="/">back</NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const nama = ref('')
const kelas = ref('')
const keperluan = ref('')
const date = ref('')
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
        keperluan: keperluan.value,
        jurusan: jurusan.value,
        nokelas: nokelas.value,
      }
    ])
  if (error) gagal.value = true
  else terkirim.value = true
}


async function bacaData() {
  const { data, error } = await supabase.from('formulir').select().order('date', { ascending: false })
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

@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;500&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Handlee&family=Josefin+Sans:wght@400;500&display=swap');

.table-dark th {
  border: 1px solid gray;
}

td {
  border: .5px solid gray;
}

td {
  background-color: #fff;
}

td:nth-child(even) {
  background-color: #AAC7D7;
}



td {
  font-family: 'Josefin Sans', sans-serif;
}

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
  margin: 30px;
  font-family: 'Josefin Sans', sans-serif;
}

.button-action {
  width: 100%;
}

/* .table-striped>tbody>tr:nth-child(odd)>th {
   background-color: red; 
 } */
</style>