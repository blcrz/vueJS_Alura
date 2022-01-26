<template>
    <div>

        <h1 class="centralizado">Alurapic</h1>

        <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre pelo título da foto">

        <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
            <meu-painel :titulo="foto.titulo">
                <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
                <botao
                tipo="button"
                rotulo="Remover"
                :confirmacao="true"
                @botaoAtivado="remove(foto)"
                estilo="perigo"
                />
            </meu-painel>
        </li>
        </ul>
    </div>
</template>

<script>

import Painel from './shared/Painel.vue';
import ImagemResponsiva from './shared/imagemResponsiva.vue'
import Botao from './shared/Botao.vue'

export default {

  components: {

    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
    'botao': Botao

  },

  data () {
    return {

      fotos: [],

      filtro: ''
    }
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {

    this.$http
      .get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  },

  methods: {

     remove(foto) {
        alert(`${foto.titulo} removida`);
    }
  }
}
</script>
<style>

  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }
</style>