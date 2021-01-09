<template>
  <v-container>
    <v-layout row wrap justify-center>
      <v-flex mt-5 class="justify-center">
        <v-card class="fields-card" width="500px">
          <v-container py-5>
            <v-layout class="field-subtitle" px-3 py-2>
              Versión
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                hide-details
                placeholder="Versión"
                outlined
                dense
                aria-disabled
                v-model="cmpData.ver">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Fecha (yyyy-MM-dd)
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                hide-details
                placeholder="Fecha (yyyy-MM-dd)"
                dense
                hint="Fecha en formato yyyy-MM-dd"
                v-model="cmpData.fecha">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              CUIT (sin guiones)
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                placeholder="CUIT (sin guiones)"
                return-masked-value
                hide-details
                v-model="cmpData.cuit">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Punto de Venta
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                hide-details
                placeholder="Punto de Venta"
                hint="Punto de venta utilizado para emitir el comprobante"
                v-model="cmpData.ptoVta">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Tipo de Comprobante
            </v-layout>
            <v-layout px-3>
              <v-select
                rounded
                outlined
                hide-details
                dense
                :items="tiposComprobantes"
                placeholder="Tipo de Comprobante (Número según tablas de la AFIP)"
                item-text="name"
                item-value="code"
                v-model="cmpData.tipoComp">
              </v-select>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Número de Comprobante
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                hide-details
                dense
                placeholder="Número de Comprobante"
                v-model="cmpData.nroCmp">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Importe
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                hide-details
                placeholder="Importe"
                hint="Hasta 13 enteros y 2 decimales"
                type="number"
                v-model="cmpData.importe">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Moneda
            </v-layout>
            <v-layout px-3>
              <v-select
                rounded
                outlined
                dense
                hide-details
                :items="monedas"
                item-value="code"
                item-text="name"
                placeholder="Moneda"
                v-model="cmpData.moneda">
              </v-select>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Cotización en pesos argentinos
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                hide-details
                placeholder="1 cuando la moneda sea pesos"
                type="number"
                v-model="cmpData.ctz">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Tipo de Documento del Receptor
            </v-layout>
            <v-layout px-3>
              <v-select
                rounded
                outlined
                dense
                hide-details
                :items="tipoDocumento"
                item-text="name"
                item-value="code"
                placeholder="Es un código que está en alguna tabla que no encontré"
                v-model="cmpData.tipoDocRec">
              </v-select>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Número de Documento del Receptor
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                hide-details
                placeholder="Hasta 20 dígitos"
                type="number"
                v-model="cmpData.nroDocRec">
              </v-text-field>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Tipo de Código de Autorización
            </v-layout>
            <v-layout px-3>
              <v-select
                :items="[{ code: 'A', name: 'CAEA' }, { code: 'E', name: 'CAE' }]"
                rounded
                outlined
                hide-details
                dense
                item-text="name"
                item-value="code"
                v-model="cmpData.tipoCodAut">
              </v-select>
            </v-layout>
            <v-layout class="field-subtitle" px-3 py-2>
              Código de Autorización para el Comprobante
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                hide-details
                placeholder="14 dígitos"
                v-model="cmpData.codAut">
              </v-text-field>
            </v-layout>
          </v-container>
        </v-card>
      </v-flex>
      <v-flex shrink mt-5 class="results-flex">
        <v-card class="fields-card" width="500px">
          <v-container>
            <v-layout justify-center>
              <v-flex class="results-title" shrink>
                QR Generado
              </v-flex>
            </v-layout>
            <v-layout justify-center>
              <vue-qrcode :value="url"></vue-qrcode>
            </v-layout>
            <v-layout justify-center >
              <v-flex class="results-url" shrink>
                <p class="results-url-text">
                  {{url}}
                </p>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>
    <!-- <p>
      {{cmpData}}
    </p>
    ------
    <p>
      {{base64Data}}
    </p>
    ------
    <p>
      {{url}}
    </p> -->
  </v-container>
</template>

<script>
// @ is an alias to /src
import tiposComprobantes from '@/data/tiposComprobantes.js'
import monedas from '@/data/monedas.js'
import tipoDocumento from '@/data/tipoDocumento.js'
import VueQrcode from 'vue-qrcode'

export default {
  name: 'Home',
  components: {
    'vue-qrcode': VueQrcode
  },
  data () {
    return {
      cmpData: {
        ver: 1,
        fecha: undefined,
        cuit: undefined,
        ptoVta: undefined,
        tipoCmp: undefined,
        nroCmp: undefined,
        importe: undefined,
        moneda: undefined,
        ctz: undefined,
        tipoDocRec: undefined,
        nroDocRec: undefined,
        tipoCodAut: 'E',
        codAut: undefined
      },
      tipoCmp: 0,
      tiposComprobantes: tiposComprobantes,
      tipoDocumento: tipoDocumento,
      monedas: monedas
    }
  },
  computed: {
    base64Data () {
      return btoa(JSON.stringify(this.cmpData))
    },
    url () {
      return 'https://www.afip.gob.ar/fe/qr/?p=' + btoa(JSON.stringify(this.cmpData))
    }
  }
}
</script>

<style lang="scss">
  .field-subtitle {
    font-size: 18px;
    font-weight: 300;
    color: steelblue;
  }
  .fields-card {
    border-radius: 16px !important;
  }
  .results-flex {
    display: flex;
    align-items: center;
  }
  .results-title {
    font-size: 50px;
    font-weight: 300;
    color: steelblue;
  }
  .results-url {
    display: flex;
    justify-content: center;
    text-align: center;
  }
  .results-url-text {
    max-width: 100%;
  }
  .justify-center {
    display: flex;
    justify-content: center;
  }
</style>
