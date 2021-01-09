<template>
  <v-container>
    <v-layout justify-center>
      <v-flex>
        <v-card class="fields-card" width="500px">
          <v-container py-5>
            <!-- <v-layout class="field-subtitle" px-3 pb-2>
              Versión
            </v-layout> -->
            <v-layout px-3>
              <v-text-field
                label="Versión"
                rounded
                outlined
                dense
                aria-disabled
                v-model="cmpData.ver">
              </v-text-field>
            </v-layout>

            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Fecha (yyyy-MM-dd)"
                hint="Fecha en formato yyyy-MM-dd"
                v-model="cmpData.fecha">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="CUIT (sin guiones)"
                return-masked-value

                v-model="cmpData.cuit">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Punto de Venta"
                hint="Punto de venta utilizado para emitir el comprobante"
                v-model="cmpData.ptoVta">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-select
                rounded
                outlined
                dense
                :items="tiposComprobantes"
                label="Tipo de Comprobante (Número según tablas de la AFIP)"
                item-text="name"
                item-value="code"
                v-model="cmpData.tipoComp">
              </v-select>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Número de Comprobante"
                v-model="cmpData.nroCmp">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Importe"
                hint="Hasta 13 enteros y 2 decimales"
                type="number"
                v-model="cmpData.importe">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-select
                rounded
                outlined
                dense
                :items="monedas"
                item-value="code"
                item-text="name"
                label="Moneda"
                v-model="cmpData.moneda">
              </v-select>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Cotización en pesos argentinos"
                hint="1 cuando la moneda sea pesos"
                type="number"
                v-model="cmpData.ctz">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Tipo de Documento del Receptor"
                hint="Es un código que está en alguna tabla que no encontré"
                v-model="cmpData.tipoDocRec">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Número de Documento del Receptor"
                hint="Hasta 20 dígitos"
                type="number"
                v-model="cmpData.nroDocRec">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Típo de Código de Autorización"
                hint="A para comprobante autorizado por CAEA, E para aut. por CAE"
                v-model="cmpData.tipoCodAut">
              </v-text-field>
            </v-layout>
            <v-layout px-3>
              <v-text-field
                rounded
                outlined
                dense
                label="Código de autorización para el comprobante"
                v-model="cmpData.codAut">
              </v-text-field>
            </v-layout>
          </v-container>
        </v-card>
      </v-flex>
      <v-flex>
        <vue-qrcode :value="url"></vue-qrcode>
      </v-flex>
    </v-layout>
    {{cmpData}}
    ------
    {{base64Data}}
    ------
    {{url}}
  </v-container>
</template>

<script>
// @ is an alias to /src
import tiposComprobantes from '@/data/tiposComprobantes.js'
import monedas from '@/data/monedas.js'
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
</style>
