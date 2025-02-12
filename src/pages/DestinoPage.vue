<template>
  <q-page class="destinos-page q-pa-md">
    <h1 class="text-h4 text-center text-primary q-mb-lg">Destinos Disponíveis</h1>

    <q-list bordered separator class="destinos-list">
      <q-item 
        v-for="destino in destinos" 
        :key="destino.id" 
        clickable 
        v-ripple
        @click="irParaDetalhes(destino.id)"
      >
        <q-item-section avatar>
          <q-img :src="destino.imagem" class="destino-img" />
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-h6 text-weight-bold">{{ destino.nome }}</q-item-label>
          <q-item-label caption class="text-grey-7">{{ destino.categoria }}</q-item-label>
        </q-item-section>

        <q-item-section side>
          <q-icon name="arrow_forward" color="primary" />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

// Importação correta das imagens
import rio from 'src/assets/rio.jpg'
import recife from 'src/assets/recife.jpg'
import salvador from 'src/assets/salvador.jpg'

export default {
  name: 'DestinoPage',
  setup() {
    const router = useRouter()

    // Lista de destinos disponíveis
    const destinos = ref([
      { id: 1, nome: 'Rio de Janeiro', categoria: 'Praia', imagem: rio },
      { id: 2, nome: 'Recife', categoria: 'Praia', imagem: recife },
      { id: 3, nome: 'Salvador', categoria: 'Cidade', imagem: salvador },
    ])

    // Função para navegar até a página de detalhes do destino
    const irParaDetalhes = (id) => {
      router.push(`/destino/${id}`)
    }

    return { destinos, irParaDetalhes }
  }
}
</script>

<style scoped>
.destinos-page {
  max-width: 600px;
  margin: 0 auto;
}

.destino-img {
  width: 60px;
  height: 60px;
  border-radius: 8px;
  object-fit: cover;
}
</style>