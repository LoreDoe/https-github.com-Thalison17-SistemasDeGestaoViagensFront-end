<template>
  <q-page class="destino-detalhes-page q-pa-md">
    <div v-if="destino" class="q-mb-lg">
      <div class="text-center q-mb-md">
        <!-- Imagem primeiro, antes do nome e descrição -->
        <q-img :src="destino.imagem" class="destino-img" />
      </div>

      <div class="text-center q-mb-md">
        <h1 class="text-h3 text-weight-bold text-primary">{{ destino.nome }}</h1>
        <p class="text-subtitle2 text-grey">{{ destino.categoria }}</p>
      </div>

      <div class="q-mb-md">
        <p class="text-body1">{{ destino.descricao }}</p>
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

// Importando as imagens corretamente
import rio from 'src/assets/rio.jpg'
import recife from 'src/assets/recife.jpg'
import salvador from 'src/assets/salvador.jpg'

export default {
  name: 'DestinoDetalhes',
  setup() {
    const route = useRoute()
    const router = useRouter()
    const destino = ref(null)

    // Lista de destinos com descrição e imagem
    const destinos = [
      {
        id: 1,
        nome: 'Rio de Janeiro',
        categoria: 'Praia',
        imagem: rio,  // Usando importação correta
        descricao: 'O Rio de Janeiro é conhecido por suas belas praias, como Copacabana e Ipanema, além do icônico Cristo Redentor. A cidade oferece uma vibrante vida cultural e vistas deslumbrantes do Pão de Açúcar.'
      },
      {
        id: 2,
        nome: 'Recife',
        categoria: 'Praia',
        imagem: recife,  // Usando importação correta
        descricao: 'Recife, a capital de Pernambuco, é famosa por suas praias, cultura rica e o bairro histórico de Olinda. É um destino perfeito para quem busca história, cultura e belas paisagens.'
      },
      {
        id: 3,
        nome: 'Salvador',
        categoria: 'Cidade',
        imagem: salvador,  // Usando importação correta
        descricao: 'Salvador é conhecida pela sua história, suas festas vibrantes e pelas praias paradisíacas. A cidade tem uma rica herança cultural, com destaque para o Pelourinho e o Elevador Lacerda.'
      }
    ]

    onMounted(() => {
      const destinoId = parseInt(route.params.id)
      destino.value = destinos.find(d => d.id === destinoId)

      console.log('Destino selecionado:', destino.value)  // Verificando no console o valor de destino
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
  border-radius: 8px;
}

.text-subtitle2 {
  font-style: italic;
}

</style>