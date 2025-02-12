<template>
  <q-page class="destino-detalhes-page q-pa-md">
    <div v-if="destino" class="q-mb-lg">
      <div class="text-center q-mb-md">
        <q-img :src="destino.imagem" class="destino-img" />
        <h1 class="text-h3 text-weight-bold text-primary">{{ destino.nome }}</h1>
        <p class="text-subtitle2 text-grey">{{ destino.categoria }}</p>
      </div>

      <div class="q-mb-md">
        <p class="text-body1">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed eget ligula a erat fermentum auctor.
          Ut sit amet ligula in lorem tincidunt malesuada. Donec aliquet ipsum vel urna laoreet, et dictum nunc iaculis.
        </p>
      </div>

      <q-btn color="primary" label="Reservar agora" @click="reservarDestino" class="q-mt-md" />
    </div>

    <div v-else class="text-center q-pa-lg">
      <q-icon name="error" size="4rem" color="grey-5" />
      <p class="text-h6 text-grey-7">Destino não encontrado</p>
    </div>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

// Importando as imagens da pasta assets
import rio from 'src/assets/img/rio.jpg'
import recife from 'src/assets/img/recife.jpg'
import salvador from 'src/assets/img/salvador.jpg'

export default {
  name: 'DestinoDetalhes',
  setup() {
    const route = useRoute()
    const router = useRouter()
    const destino = ref(null)

    const destinos = [
      { id: 1, nome: 'Rio de Janeiro', categoria: 'Praia', imagem: rio },
      { id: 2, nome: 'Pernambuco', categoria: 'Montanha', imagem: recife },
      { id: 3, nome: 'Bahia', categoria: 'Cidade', imagem: salvador }
    ]

    onMounted(() => {
      const destinoId = parseInt(route.params.id)
      destino.value = destinos.find(d => d.id === destinoId)
    })

    const reservarDestino = () => {
      console.log('Reserva realizada para:', destino.value.nome)
      router.push('/')
    }

    return { destino, reservarDestino }
  }
}
</script>

<style scoped>
.destino-detalhes-page {
  max-width: 800px;
  margin: 0 auto;
}

.destino-img {
  height: 250px;
  object-fit: cover;
}

.text-subtitle2 {
  font-style: italic;
}
</style>