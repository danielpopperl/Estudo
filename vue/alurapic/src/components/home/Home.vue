<template>
  <div>
    <h1 class="centralizado">Cachorro</h1>

      <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="Digite o nome da imagem" >

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of filtroFotos" :key="foto">
        <meu-painel :titulo="foto.titulo">
            <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>

            <meu-botao
            rotulo="REMOVER"
            tipo="button"
            @botaoAtivado="remove(foto, $event)"
            estilo="perigo"/>
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>

import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/imagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue'

export default {

  components: {
    'meu-painel' : Painel,
    'imagem-responsiva' : ImagemResponsiva,
    'meu-botao' : Botao
  },

  data() {
    return {
      fotos: [],
      filtro: ''
    };
  },

  computed: {
    filtroFotos() {
      if(this.filtro) {
        let filter = new RegExp(this.filtro, 'i');
        return this.fotos.filter(foto => filter.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then((res) => res.json())
      .then(
        (fotos) => (this.fotos = fotos),
        (error) => console.log(error)
      );
  },

  methods: {
    remove(foto, $event) {
      alert('foto ' + foto.titulo + ', removida às: ' + $event)
    }
  }
};

</script>

<style lang="scss">

.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}


/* estilo do painel */

.painel {
  padding: 0 auto;
  border: solid 2px grey;
  display: inline-block;
  margin: 5px;
  box-shadow: 5px 5px 10px grey;
  width: 200px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  text-align: center;
  border: solid 2px;
  background: lightblue;
  margin: 0 0 15px 0;
  padding: 10px;
  text-transform: uppercase;
}
</style>
