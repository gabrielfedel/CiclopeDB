<template>
<right-sidebar id="info-ipes-right-sidebar">
  <template slot="tabs">
      <div class='px12 py12 bg-blue-faint txt-s'>
          <div class="txt-l txt-bold mb-neg3">
              <div class='grid'>
                  <div class='col col--1 block cursor-pointer' style="margin: auto;" v-on:click="backToInitialSidebar()">
                      <svg class="icon h24 w24 mx-auto mx-auto">
                          <use xlink:href="#icon-arrow-left"></use>
                      </svg>
                  </div>
                  <div class='col col--10'>
                      <div class="txt-l txt-bold mb-neg3">{{ nome }}</div>
                  </div>
                  <div class='col col--1 block cursor-pointer' style="margin: auto;" v-on:click="closeSidebar()">
                      <svg class="icon h24 w24 mx-auto mx-auto">
                          <use xlink:href="#icon-close"></use>
                      </svg>
                  </div>
              </div>
          </div>
      </div>
    <ul class="tabs bg-blue border-b border--white flex-parent h40 txt-bold txt-s"
            style="justify-content:space-around;height: 35px;">
            <li class="mb-neg1 px12 py6 border-b border--white border--white-on-active color-lighten50 color-white-on-active color-lighten75-on-hover">
                <a href="#info-ipes-tab-info-gerais">Informações Gerais</a>
            </li>
            <li id="ipes-tab-dados" class="hide-visually mb-neg1 px12 py6 border-b border--white border--white-on-active color-lighten50 color-white-on-active color-lighten75-on-hover">
                <a href="#info-ipes-tab-dados">Dados</a>
            </li>
            <li id="ipes-tab-linha-tempo" class="hide-visually mb-neg1 px12 py6 border-b border--white border--white-on-active color-lighten50 color-white-on-active color-lighten75-on-hover">
                <a href="#info-ipes-tab-linha-tempo">Linha do Tempo</a>
            </li>
        </ul>
  </template>
  <template slot="content">
    <div class='px12 py12 scroll-auto set-height'>
      <div id="info-ipes-tab-info-gerais" v-show="sigla">
        <div class='grid'>
            <!--Logradouro-->
            <div class='col col--1 block' style="margin: auto;" v-if="endereco.logradouro.length > 2">
                <svg class="icon h24 w24 mx-auto mx-auto">
                    <use xlink:href="#icon-street"></use>
                </svg>
            </div>
            <div class='col col--11 my6' v-if="endereco.logradouro.length > 2">
                <div class="txt-s txt-bold mb-neg3">
                    <p>Endereço</p>
                </div>
                <div class="txt-m">
                    <p class="txt-capitalize">{{ endereco.logradouro | allLowercase }}</p>
                </div>
            </div>
            <!--Fim do Logradouro-->
            <!--Bairro-->
            <div class='col col--1 block' style="margin: auto;" v-if="bairro != ''">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-home"></use>
                </svg>
            </div>
            <div class='col col--11 my6' v-if="bairro != ''">
                <div class="txt-s txt-bold mb-neg3">
                    <p>Bairro</p>
                </div>
                <div class="txt-m">
                    <p class="txt-capitalize">{{ bairro | allLowercase }}</p>
                </div>
            </div>
            <!--Fim do Bairro-->
            <!--Cidade-->
            <div class='col col--1 block' style="margin: auto;">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-map"></use>
                </svg>
            </div>
            <div class='col col--11 my6'>
                <div class="txt-s txt-bold mb-neg3"><p>Cidade</p></div>
                <div class="txt-m">
                    <p>{{ cidade }}</p>
                </div>
            </div>
            <!--Fim do Cidade-->
            <!--Estado-->
            <div class='col col--1 block' style="margin: auto;">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-globe"></use>
                </svg>
            </div>
            <div class='col col--11 my6'>
                <div class="txt-s txt-bold mb-neg3"><p>Estado</p></div>
                <div class="txt-m">
                    <p>{{ estado }}</p>
                </div>
            </div>
            <!--Fim do Estado-->
            <!--CEP-->
            <div class='col col--1 block' style="margin: auto;" v-if="cep.length > 2">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-marker"></use>
                </svg>
            </div>
            <div class='col col--11 my6' v-if="cep.length > 2">
                <div class="txt-s txt-bold mb-neg3"><p>CEP</p></div>
                <div class="txt-m">
                    <p>{{ cep | formataCep }}</p>
                </div>
            </div>
            <!--Fim do CEP-->
            <!--Telefone-->
            <div class='col col--1 block' style="margin: auto;" v-if="telefone.length > 3">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-mobile"></use>
                </svg>
            </div>
            <div class='col col--11 my6' v-if="telefone.length > 3">
                <div class="txt-s txt-bold mb-neg3"><p>Telefone</p></div>
                <div class="txt-m">
                    <p>{{ telefone | formataTelefone }}</p>
                </div>
            </div>
            <!--Fim do Telefone-->
            <!--URL-->
            <div class='col col--1 block' style="margin: auto;" v-if="url !== ''">
                <svg class="icon h24 w24 mx-auto">
                    <use xlink:href="#icon-info"></use>
                </svg>
            </div>
            <div class='col col--11 my6' v-if="url !== ''">
                <div class="txt-s txt-bold mb-neg3"><p>URL</p></div>
                <div class="txt-m">
                    <a :href="url" class="link">{{ url }}</a>
                </div>
            </div>
            <!--Fim da URL-->
            <div v-html="infoIpesText"></div>
        </div>
    </div>
        <div id="info-ipes-tab-dados">
            <table id="ipes-info-table" class="display" cellspacing="0" width="100%">
                <thead>
                <tr>
                    <th>Sigla</th>
                    <th>Estado</th>
                    <th>Polo</th>
                    <th>Estado</th>
                </tr>
                </thead>
            </table>

            <hr class='txt-hr'>

            <!--carrega os gráficos-->
            <div id="graphContainer">
                <div class="txt-m txt-bold mb6">
                    <p>Número de polos por estado</p>
                </div>
            </div>
        </div>

      <div id="info-ipes-tab-linha-tempo">
          <div id="timeline"></div>
      </div>
    </div>

  </template>
</right-sidebar>
</template>

<script>
import { EventBus } from "../eventBus";
import { loadChart, processBarChartIpesWithSiglaIpes } from '../functions';
import axios from 'axios';

export default {
  data() {
    return {
      id: "",
      sigla: "",
      nome: "",
      endereco: {
        logradouro: "",
        numero: "",
        complemento: ""
      },
      bairro: "",
      cidade: "",
      estado: "",
      cep: "",
      telefone: "",
      url: "",
      isVisible: false,
      infoIpesText: ''
    };
  },
  mounted() {
    $("#info-ipes-right-sidebar").tabs({show: 'fade', hide: 'fade', active: 0,
      activate: function( event, ui ) {
      // ajusta o tamanho da janela para mostrar a timeline corretamente
        let resize = new Event('resize');
        window.dispatchEvent(resize);
        if (ui.newTab[0].id === "ipes-tab-linha-tempo") {
          window.dispatchEvent(resize);
        }
      }
    });

    EventBus.$on("infoIpes", infoIpes => {
      this.setInfoIpes(infoIpes);
      this.loadIpesDataTable(infoIpes);
      this.loadTimeline(infoIpes);
      this.loadGraph(infoIpes);
    });
    EventBus.$on("switchInfoIpes", isVisible => {
      this.isVisible = isVisible
    });

    $('#polosBarChart').remove();
    $('#graphContainer').append('<canvas id="polosBarChart"><canvas>');

  },
  watch: {
    isVisible() {
      if(this.isVisible) {
        $('#initial-sidebar').addClass("hide-visually");
        $("#info-ipes-right-sidebar").removeClass("hide-visually");
      } else {
        $('#initial-sidebar').removeClass("hide-visually");
        $("#info-ipes-right-sidebar").addClass("hide-visually");
      }
    }
  },
  methods: {
    backToInitialSidebar: function() {
      $('#initial-sidebar').removeClass("hide-visually");
      $("#info-ipes-right-sidebar").addClass("hide-visually");
    },
    closeSidebar: function() {
      $('#initial-sidebar').addClass("hide-visually");
      $("#info-ipes-right-sidebar").addClass("hide-visually");
    },
    loadIpesDataTable: function(infoIpes) {
      let ipesTable = $('#ipes-info-table').DataTable({
        "retrieve": true,
        "ajax": {
          "url": "./static/json/ipesdatatable.json",
          "dataSrc": "data"
        },
        "language": {
          "url": "./static/json/datatables_pt-br.json",
        },
        "columns": [
          { "data": "sigla_ipes" },
          { "data": "estado_ipes" },
          { "data": "nome_polo" },
          { "data": "estado_polo" }
        ],
        "columnDefs": [
          { "width": "40%", "targets": 2 },
          { "width": "10%", "targets": 3 },
          {
            "targets": [0, 1],
            "visible": false,
          }
        ]
      }).columns(0)
        .search("^" + infoIpes.sigla + "$", true, false, true)
        .draw();
    },
    loadTimeline: function(infoIpes) {
      $.getJSON("./static/json/linhas.json", function (data){
        $('#ipes-tab-linha-tempo').addClass("hide-visually");
        $('#ipes-timeline-embed').css( "display", "none" );
        $.each( data, function( key, val ) {
          if(key === infoIpes.sigla) {
            var options = {
              initial_zoom: 1,
              width: 150,
              height: 450,
              is_embed: true
            };
            $('#ipes-tab-linha-tempo').removeClass("hide-visually");
            // remove alguma timeline anterior
            $('#ipes-timeline-embed').remove();
            // adiciona uma div e cria a timeline na primeira aba
            $('#info-ipes-tab-info-gerais').append('<div id="ipes-timeline-embed" style="width: 100%;height: 450px;display:block;"></div>');
            window.timeline = new TL.Timeline('ipes-timeline-embed', val, options);
            // adiciona a div da primeira aba na terceira aba
            $('#ipes-timeline-embed').appendTo('#timeline');
          }
        })
      });
    },
    loadGraph(infoIpes) {
      $('#polosBarChart').remove();
      $('#graphContainer').append('<canvas id="polosBarChart"><canvas>');

      var myBarChart = loadChart("polosBarChart", "bar", "Polos");
      processBarChartIpesWithSiglaIpes(myBarChart, infoIpes.sigla);
    },
    setInfoIpes: function(infoIpes) {
      $("#info-ipes-right-sidebar").tabs("option", "active", 0).removeClass("hide-visually");
      $('#initial-sidebar').addClass("hide-visually");

      this.id = null;
      this.sigla = infoIpes.sigla;
      this.arquivo = infoIpes.arquivo;
      this.nome = infoIpes.sigla;
      this.endereco.logradouro = infoIpes.logradouro;
      this.bairro = infoIpes.bairro;
      this.cidade = infoIpes.cidade;
      this.estado = infoIpes.estado;
      this.cep = infoIpes.cep;
      this.telefone = infoIpes.telefone;
      this.url = infoIpes.url;

      let ipesFiles = ['uel', 'uema', 'ufc', 'uff', 'ufmt', 'ufop', 'ufpa', 'ufsc', 'ufscar'];

      for (let i = 0; i < ipesFiles.length; i++) {
        if(ipesFiles[i] === infoIpes.sigla.toLowerCase()) {
          axios.get('static/ipes/' + infoIpes.sigla.toLowerCase() + '.html')
            .then(response => {
              // JSON responses are automatically parsed.
              this.infoIpesText = response.data
            })
            .catch(e => {
              this.errors.push(e)
            })
        } else {
          this.infoIpesText = ''
        }
      }
    }
  },
  filters: {
    formataCep: function(cep) {
      if (!cep) return "";
      var primeiraparte = cep.substr(0, 5);
      var segundaparte = cep.substr(5, 3);
      var cepcompleto = primeiraparte + "-" + segundaparte;
      return cepcompleto;
    },
    formataTelefone: function(telefone) {
      if (!telefone) return "";
      var primeiraparte = telefone.substr(0, 9);
      var segundaparte = telefone.substr(9, 4);
      var telefonecompleto = primeiraparte + "-" + segundaparte;
      return telefonecompleto;
    },
    formataEndereco: function(logradouro, numero) {
      if (!logradouro || !numero) return "";
      return logradouro + ", " + numero;
    },
    allLowercase: function(txt) {
      if (!txt ) return "";
      return txt.toLowerCase()
    }
  }
};
</script>

<style>

</style>


