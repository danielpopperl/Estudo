<template>
  <button class="botao" :class=estiloBotao :type="tipo" @click="remove()">{{ rotulo }}</button>
</template>

<script>
export default {
  props: ['tipo', 'rotulo', 'estilo'],

  methods: {
    remove() {
      if(confirm('Confirma?')) {
        this.$emit('botaoAtivado', new Date());
      }
    }
  },

  computed: {
    estiloBotao() {
      if(this.estilo == 'padrao') return 'botao-padrao';
      if(this.estilo == 'perigo') return 'botao-perigo'
    }
  }

}
</script>

<style scoped>
  .botao {
    display: inline-block;
    padding: 10px;
    border-radius: 3px;
    margin: 10px;
    font-size: 1.2em;
  }

  .botao-perigo {
    background: firebrick;
    color: floralwhite;
  }

  .botao-padrao {
    background: darkcyan;
    color: white;
  }
</style>
