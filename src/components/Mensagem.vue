<template>
  <div class="mensagem" :class="{verde: verde}">
    {{ conteudo }}
    <span>{{ horario }}</span>
  </div>
</template>

<script>
export default {
  name: 'Mensagem',
  props: ['conteudo', 'horario', 'verde']
}
</script>

<style lang="scss">

  .verde{
    background: #005C4B !important;
    color: #FFF;
    align-self: flex-end;
    
  }

  .mensagem{
    font-size: 14px;
    box-shadow: rgba(0, 0, 0, 0.13) 0px 1px 0.5px 0px;
    background: white;
    margin: 5px 100px;
    padding: 5px 10px;
    border-radius: 5px;
    width: fit-content;

    span{
        margin-left: 25px;
        font-size: 11px;
    }
  }

</style>