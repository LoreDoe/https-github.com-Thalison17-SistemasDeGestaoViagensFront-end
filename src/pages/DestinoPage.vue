<template>
    <q-page class="destinos-page q-pa-md">
      <div class="text-center q-mb-lg">
        <h1 class="text-h3 text-weight-bold text-primary">Destinos</h1>
        <p class="text-subtitle1">Encontre os melhores lugares para sua próxima viagem</p>
      </div>
  
      <div class="row q-col-gutter-md q-mb-md">
        <div class="col-12 col-md-6">
          <q-input v-model="search" outlined dense label="Buscar destino" placeholder="Digite o nome do destino">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </div>
        <div class="col-12 col-md-6">
          <q-select v-model="categoryFilter" :options="categoryOptions" outlined dense label="Categoria" />
        </div>
      </div>
  
      <div class="row q-col-gutter-md">
        <div v-for="destino in filteredDestinos" :key="destino.id" class="col-12 col-md-4">
          <q-card class="destino-card">
            <q-img :src="destino.imagem" class="destino-img" />
            <q-card-section>
              <div class="text-h6">{{ destino.nome }}</div>
              <div class="text-subtitle2 text-grey">{{ destino.categoria }}</div>
              <q-btn color="primary" label="Ver Detalhes" @click="verDetalhes(destino.id)" class="q-mt-sm" />
            </q-card-section>
          </q-card>
        </div>
      </div>
  
      <div v-if="filteredDestinos.length === 0" class="text-center q-pa-lg">
        <q-icon name="location_off" size="4rem" color="grey-5" />
        <p class="text-h6 text-grey-7">Nenhum destino encontrado</p>
      </div>
    </q-page>
  </template>
  
  <script>
  import { ref, computed } from 'vue'
  import { useRouter } from 'vue-router'
  
  export default {
    setup() {
      const router = useRouter()
      const search = ref('')
      const categoryFilter = ref('Todos')
  
      const categoryOptions = ['Todos', 'Praia', 'Montanha', 'Cidade', 'Campo']
  
      const destinos = ref([
        { id: 1, nome: 'Rio de Janeiro', categoria: 'Praia', imagem: 'https://source.unsplash.com/400x300/?rio' },
        { id: 2, nome: 'Campos do Jordão', categoria: 'Montanha', imagem: 'https://source.unsplash.com/400x300/?mountain' },
        { id: 3, nome: 'São Paulo', categoria: 'Cidade', imagem: 'https://source.unsplash.com/400x300/?city' },
      ])
  
      const filteredDestinos = computed(() => {
        return destinos.value.filter(destino => {
          const matchSearch = search.value === '' || destino.nome.toLowerCase().includes(search.value.toLowerCase())
          const matchCategory = categoryFilter.value === 'Todos' || destino.categoria === categoryFilter.value
          return matchSearch && matchCategory
        })
      })
  
      const verDetalhes = (id) => {
        router.push(`/destinos/${id}`)
      }
  
      return { search, categoryFilter, categoryOptions, filteredDestinos, verDetalhes }
    }
  }
  </script>
  
  <style scoped>
  .destinos-page {
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .destino-card {
    transition: transform 0.2s ease;
  }
  
  .destino-card:hover {
    transform: translateY(-2px);
  }
  
  .destino-img {
    height: 200px;
    object-fit: cover;
  }
  </style>