<template>
  <div class="container">
      <img class="logosmk" src="@/assets/img/logosmkn4.png" />
    <div class="title">
      <h1 class="judul">Catatan Daftar Pengunjung Perpustakaan Digital</h1>
      <!-- <img class="logoperpus" src="@/assets/img/logoperpus.png"> -->
    </div>
    <img class="homeimg" src="@/assets/img/home.png">
    <button class="submitbtn" onclick="myFunction()">Isi Sekarang</button>
    <button class="seedetail">See Detail</button>
  </div>
</template>
    <!-- <div v-for="(formulir, index) in datas" :key="formulir.id">
      <div>{{ index + 1 }}</div>
      <div>{{ formulir.nama }}</div>
      <div>{{ formulir.kelas }}</div>
      <div>{{ formulir.keperluan }}</div>
      <div>{{ formulir.date }}</div>
    </div> -->


<script>
  export default {
  }

  function myFunction() {
    alert("terimakasih telah mengisi ");
}

</script>

<script setup>

const supabase = useSupabaseClient()
const datas = ref([])

async function getData() {
  const { data } = await supabase
  .from("formulir")
  .select()
  datas.value = data
}

onMounted(() => {
  getData()
})

</script>



<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@300&display=swap');


  .container{
    background-color:#28353D;
    width: 100%;
    height: 100%;
  }



  .judul{
    text-align: center;
    color: white;
    font-style: italic;
    font-weight: 10;
    font-size: 40px;
  }


  .homeimg{
  width: 500px;
  height: 400px;
  flex-shrink: 0;
  margin-left: 50px;
  }


  .logosmk{
  width: 83px;
  height: 84px;
  padding-top: 20px;
  padding-left: 10px;
  }

  .logoperpus{
    width: 100px;
    height: 100px;
    padding-left: 75%;
  }

  .submitbtn{
  border-radius: 100px;
  background: #E6E6E6;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  width: 170px;
  height: 70px;
  transform: rotate(-0.812deg);
  flex-shrink: 0;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-left: 65%;
  font-family: 'Josefin Sans', sans-serif;
  }


  .seedetail{
  border-radius: 17px;
  background: #D9D9D9;
  width: 170px;
  height: 70px;
  transform: rotate(-0.812deg);
  flex-shrink: 0;
  color: #000;
  text-align: center;
  font-size: 20px;
  margin-left: 50px;
  margin-bottom: 15px;
  font-family: 'Josefin Sans', sans-serif;
  }

</style>