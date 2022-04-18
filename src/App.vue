<template>
  <div id="#app">
    <section class="section">
      <div class="container">
        <div class="columns">

          <div class="column is-3 lista-de-conversas">
            <div class="barra-superior" />
            <div
              class="item"
              v-for="(conversa, indice) in conversas"
              :key="indice"
              @click="indiceAtivo = indice">
              
              <div class="title is-6">
                {{ conversa.usuario }}
              </div>
              <div class="subtitle is-6">
                Última mensagem ...
              </div>
            </div>
          </div>

          <div class="column conversa-ativa">
            <div class="barra-superior" >
              <span>{{ conversas[indiceAtivo].usuario }}</span>
            </div>

            <div class="lista-mensagens">
              <Mensagem 
                v-for="(mensagem, indice) in conversas[indiceAtivo].mensagens"
                :key="indice"
                :conteudo="mensagem.conteudo"
                :horario="mensagem.horario"
                :verde="mensagem.verde"
                
              />
            </div>
            <div class="barra-inferior">
              <input 
                class="input" 
                type="text" 
                placeholder="Insira sua mensagem" 
                v-model="conteudoNovaMensagem"
                v-on:keyup.enter="enviarMensagem" 
              />
            </div>
          </div>

        </div>
      </div>
    </section>
  </div>
</template>

<script>

import './styles/global.scss';
import Mensagem from './components/Mensagem.vue';
import conversasIniciais from './dados/Dados';

export default {
  name: 'App',
  components: {
    Mensagem
  },
  data: function () {
    return {
      conversas: conversasIniciais,
      indiceAtivo: 0,
      conteudoNovaMensagem: ''
    }
  },
  methods: {
    enviarMensagem: function(){
      let horarioAtual = new Date().getHours() + ":" + new Date().getMinutes();

      let novaMensagem = {
        horario: horarioAtual,
        conteudo: this.conteudoNovaMensagem,
        verde: true
      };

      this.conversas[this.indiceAtivo].mensagens.push(novaMensagem)

      this.conteudoNovaMensagem = '';
    }
  }
}
</script>

<style lang="scss">
  #app{
    
  }
  .columns{
    min-height: 90vh;
    box-shadow: 0 3rem 3rem -1rem rgba(10, 10, 10, .2);
    .column{
      padding: 0;
    }
    .lista-de-conversas{
      color: #FFF;
      background: #111B21;
    }
    .conversa-ativa {
      background: #222E35;
      .lista-mensagens{
        height: 85%;
        display: flex;
        justify-content: flex-end;
        flex-direction: column;
      }
      .barra-inferior{
        bottom: 0;
        width: 77%;
        padding: 10px;
        position: absolute;
        background: #14181b;
      }
      input{
        border: none;
        padding: 10px;
        margin: 0 50px;
        width: 90%;
        border-radius: 15px;
        font-size: 16px;
        background: #222E35;
        color: #fff;
        &::placeholder{
          color: rgb(174, 170, 170);
        }
      }
    }
    .barra-superior{
      color: #FFF;
      margin: 0;
      height: 50px;
      background: #222E35;
      border-right: 1px solid #000000;
      border-bottom: 1px solid #000000;
      span{
        line-height: 50px;
        margin-left: 25px;
        font-weight: 500;

      }
    }
    
    .item{
      border-bottom: 1px solid rgb(163, 160, 160);
      padding: 15px 30px;
      margin-bottom: 0 !important;
      &:hover{
        background: #202C33;
        cursor: pointer;
      }
      .title{
        color: #FFF;

      }
      .subtitle{
        color: rgb(163, 160, 160);
      }
    }
  }
</style>