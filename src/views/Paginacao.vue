<template>
  <div class="paginacao">
    <div class="row">
      <div class="col-lg-3 pr-1">
        <div class="card" style="height: 100%;">
          <div class="card-body">
            <h6 class="card-title">Criar Processo</h6>
            <form @submit.prevent="criarProcesso">
              <div class="form-group">
                <label for="exampleInputEmail1">Processo:</label>
                <input
                  type="text"
                  required
                  class="form-control"
                  id="processo"
                  name="processo"
                  @change="$event.target.value = $event.target.value.toUpperCase()"
                  maxlength="1"
                />
              </div>
              <div class="form-group">
                <label for="exampleInputPassword1">Código:</label>
                <input
                  type="number"
                  required
                  class="form-control"
                  id="codigo"
                  name="codigo"
                  @change="validaCampo"
                />
              </div>
              <div class="form-group">
                <label for="exampleInputPassword1">Dados:</label>
                <input
                  type="number"
                  required
                  class="form-control"
                  id="dado"
                  name="dado"
                  @change="validaCampo"
                />
              </div>
              <div class="form-group">
                <label for="exampleInputPassword1">Pilha:</label>
                <input
                  type="number"
                  required
                  class="form-control"
                  id="pilha"
                  name="pilha"
                  @change="validaCampo"
                />
              </div>
              <button type="submit" class="btn btn-success">Criar</button>
            </form>
          </div>
        </div>
      </div>
      <div class="col-lg-9 pl-1">
        <div class="row">
          <div class="col-lg-12">
            <div class="card">
              <div class="card-body">
                <h6 class="card-title">Processos</h6>
                <span v-for="item in arrProcesso">
                  <button
                    class="btn btn-secondary btn-sm distancia-botao-processos"
                    @click="processoSelecionado = item.id"
                    :style="processoSelecionado == item.id ? 'font-weight: bold; text-decoration: underline' : null"
                  >{{ item.sig_processo }}</button>
                  <!--<button
                    class="btn btn-secondary btn-sm"
                    @click="recarregarPagina"
                  >Remover Processos</button>-->
                </span>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-lg-12">
            <div class="card">
              <div class="card-body">
                <div class="row">
                  <div class="col-lg-4 pr-1">
                    <h6 v-if="arrProcesso.length === 0">Segmentos</h6>
                    <span v-if="arrProcesso.length > 0">
                      <h6>Segmento 00 - Código</h6>
                      <Table
                        :arrDados=" arrProcesso[processoSelecionado].codigo.segmentos"
                        :arrColunas="['Segmento','Deslocamento', 'Bytes']"
                        :corFundo="arrProcesso[processoSelecionado].codigo.corFundo"
                      />
                      <h6>Segmento 01 - Dados</h6>
                      <Table
                        :arrDados=" arrProcesso[processoSelecionado].dado.segmentos"
                        :arrColunas="['Segmento','Deslocamento', 'Bytes']"
                        :corFundo="arrProcesso[processoSelecionado].dado.corFundo"
                      />
                      <h6>Segmento 10 - Pilha</h6>
                      <Table
                        :arrDados=" arrProcesso[processoSelecionado].pilha.segmentos"
                        :arrColunas="['Segmento','Deslocamento', 'Bytes']"
                        :corFundo="arrProcesso[processoSelecionado].pilha.corFundo"
                      />
                    </span>
                  </div>
                  <div class="col-lg-4 pl-1">
                    <h6>Tabela de Segmentos</h6>
                    <Table
                      v-if="arrTabelaSegmentos.length > 0"
                      :arrDados="arrTabelaSegmentos[processoSelecionado]"
                      :arrColunas="['Segmento','Base', 'Limite']"
                    />
                  </div>
                  <div class="col-lg-4 pl-1">
                    <h6>Memória Física</h6>
                    <Table :arrDados="arrMemoriaFisica" :arrColunas="['Endereço','Byte']" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <small class="form-text text-muted">*Tamanho da Memória Física Fixado: 16 Bytes</small>
  </div>
</template>

<script>
import Table from "../components/Table";

export default {
  name: "paginacao",
  components: { Table },
  data: function() {
    return {
      processoSelecionado: 0,
      arrProcesso: [
        /*
        {
          sig_processo : ''
          codigo : [

          ],
          dados : [

          ],
          pilha : [

          ]
        }
      */
      ],
      arrTabelaSegmentos: [
        /*
        {
          00 : {base: '', limite: ''}
          01 : {base: '', limite: ''}
          10 : {base: '', limite: ''}
        }
        */
      ],
      /* Também Representa os Deslocamentos dos segmentos*/
      arrMemoriaFisica: [
        {
          endereco: "0000",
          byte: ""
        },
        {
          endereco: "0001",
          byte: ""
        },
        {
          endereco: "0010",
          byte: ""
        },
        {
          endereco: "0011",
          byte: ""
        },
        {
          endereco: "0100",
          byte: ""
        },
        {
          endereco: "0101",
          byte: ""
        },
        {
          endereco: "0110",
          byte: ""
        },
        {
          endereco: "0111",
          byte: ""
        },
        {
          endereco: "1000",
          byte: ""
        },
        {
          endereco: "1001",
          byte: ""
        },
        {
          endereco: "1010",
          byte: ""
        },
        {
          endereco: "1011",
          byte: ""
        },
        {
          endereco: "1100",
          byte: ""
        },
        {
          endereco: "1101",
          byte: ""
        },
        {
          endereco: "1110",
          byte: ""
        },
        {
          endereco: "1111",
          byte: ""
        }
      ]
    };
  },
  methods: {
    criarProcesso(event) {
      const sig_processo = event.target.processo.value;
      const codigo = event.target.codigo.value;
      const dado = event.target.dado.value;
      const pilha = event.target.pilha.value;

      //Verifica se a sigla/nome do processo já foi cadastrado
      for (const item of this.arrProcesso) {
        if (item.sig_processo === sig_processo) {
          alert(`Processo "${sig_processo}" já cadastrado.`);
          return;
        }
      }

      //Verifica se há espaço na memória física
      if (
        parseInt(codigo) + parseInt(dado) + parseInt(pilha) >
        this.arrMemoriaFisica.filter(item => item.byte === "").length
      ) {
        alert("Epaço insuficiente na memória física.");
        return;
      }

      const novoProcesso = {
        id: this.arrProcesso.length,
        sig_processo,
        codigo: {
          segmentos: this.criarSegmento(codigo, "codigo"),
          corFundo: this.geraCorAleatoria()
        },
        dado: {
          segmentos: this.criarSegmento(dado, "dado"),
          corFundo: this.geraCorAleatoria()
        },
        pilha: {
          segmentos: this.criarSegmento(pilha, "pilha"),
          corFundo: this.geraCorAleatoria()
        }
      };

      //Adiciona o novo processo na lista
      this.arrProcesso.push(novoProcesso);

      //Preencher Memoria fisica e monta a tabela de segmentos
      this.preencherMemoriaFisica(novoProcesso);

      //Selecionar o processo atual
      this.processoSelecionado = this.arrProcesso.length - 1;

      //Limpa Campo
      this.limparCampos(event);
    },
    criarSegmento(numberTamanho, strSegmento) {
      var arrSegmento = [];
      var objAux = {};
      for (var i = 0; i < numberTamanho; i++) {
        objAux.segmento = "";
        objAux.deslocamento = this.arrMemoriaFisica[i].endereco;
        if (strSegmento === "codigo") {
          objAux.bytes = "C" + (i + 1);
        } else if (strSegmento === "dado") {
          objAux.bytes = "D" + (i + 1);
        } else if (strSegmento === "pilha") {
          objAux.bytes = "P" + (i + 1);
        }
        arrSegmento.push(objAux);
        objAux = {};
      }
      return arrSegmento;
    },
    preencherMemoriaFisica(novoProcesso) {
      const self = this;
      function preencher(arr, corFundo) {
        var aux = 0;
        var base;
        var limite;
        const memoriaFisicaLivre = self.arrMemoriaFisica.filter(
          i => i.byte === ""
        );
        for (var m = 0; m < memoriaFisicaLivre.length; m++) {
          if (aux === 0) {
            //base
            base = memoriaFisicaLivre[m].endereco;
          }
          for (var i = aux; i < arr.length; i++) {
            memoriaFisicaLivre[m].byte = arr[i].bytes;
            aux++;
            break;
          }
          memoriaFisicaLivre[m].corFundo = corFundo;
          if (aux == arr.length) {
            //limite
            if (m === memoriaFisicaLivre.length - 1)
              limite = memoriaFisicaLivre[m].endereco;
            else limite = memoriaFisicaLivre[m + 1].endereco;
            break;
          }
        }
        return {
          base,
          limite
        };
      }

      const codigoBaseLimite = preencher(
        novoProcesso.codigo.segmentos,
        novoProcesso.codigo.corFundo
      );

      const dadoBaseLimite = preencher(
        novoProcesso.dado.segmentos,
        novoProcesso.dado.corFundo
      );

      const pilhaBaseLimite = preencher(
        novoProcesso.pilha.segmentos,
        novoProcesso.pilha.corFundo
      );

      //Preenche tabela de segmentos
      this.arrTabelaSegmentos.push([
        {
          segmento: "00",
          base: codigoBaseLimite.base,
          limite: codigoBaseLimite.limite,
          corFundo: novoProcesso.codigo.corFundo
        },
        {
          segmento: "01",
          base: dadoBaseLimite.base,
          limite: dadoBaseLimite.limite,
          corFundo: novoProcesso.dado.corFundo
        },
        {
          segmento: "10",
          base: pilhaBaseLimite.base,
          limite: pilhaBaseLimite.limite,
          corFundo: novoProcesso.pilha.corFundo
        }
      ]);
    },
    geraCorAleatoria() {
      const hexadecimais = "0123456789ABCDEF";
      var cor = "#";
      for (var i = 0; i < 6; i++)
        cor += hexadecimais[Math.floor(Math.random() * 16)];
      return cor;
    },
    validaCampo(event) {
      const ref = event.target
      if (ref.value <= 0) {
        alert(
          `Campo "${ref.name.toUpperCase()}" deve ser maior que zero.`
        );
        ref.value =
          ref.value <= 0 ? null : ref.value;

        ref.focus()
      }
    },
    limparCampos() {
      event.target.processo.value = null;
      event.target.codigo.value = null;
      event.target.dado.value = null;
      event.target.pilha.value = null;
    },
    recarregarPagina() {
      location.reload();
    }
  }
};
</script>

<style scoped>
.distancia-botao-processos {
  margin-right: 2px;
}
</style>
