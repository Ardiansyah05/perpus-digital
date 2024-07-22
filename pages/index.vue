<template>
  <div class="container-fluid">
    <div class="row my-5">
      <div class="col-lg-6">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-4" data-v-98588d9b="">
            <div class="card-body">
              <h2>Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
      <div class="col-lg-6">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-4">
            <div class="card-body">
              <h2>Cari Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>.
  <h2 class="justify-content-between">STATISIK</h2>
  <div class="container-fluid">
    <div class="row justify-content-evenly rounded-2">
      <div class="col-5">
        <div class="raccing">
          <nuxt-link to="pengunjung">
            <h2>{{ visitors.length }} Pengunjung </h2>
          </nuxt-link>
        </div>
      </div>
      <div class="col-5">
        <div class="raccing1">
          <h2>{{ books.length }} Buku</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  height: 174px;
  box-shadow: 1px 1px 10px #424242;
}

.card.bg-pengunjung {
  background-image: url("../assets/img/bg-home-kunjungan.webp");
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.card.bg-buku {
  background-image: url("../assets/img/bg-home-cari-buku.jpeg");
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.raccing {
  height: 174px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #BDFF00;
}

.raccing1 {
  height: 174px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #00FFA3;
}
</style>
<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])
const books = ref([])

const getPengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select('*, keanggotaan(*), keperluan(*)')
  if (data) visitors.value = data
}

const getBooks = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  if (data) books.value = data
}

onMounted (() => {
  getPengunjung()
  getBooks()
})


</script>
