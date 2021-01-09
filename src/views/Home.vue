<template>
  <v-container>
    <v-card width="500px">
      <v-container>
        <v-layout>
          <v-text-field
            label="Versión"
            aria-disabled
            v-model="cmpData.ver">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Fecha (yyyy-MM-dd)"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.fecha">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="CUIT (sin guiones)"
            aria-disabled
            return-masked-value
            mask="##-########-##"
            v-model="cmpData.cuit">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Punto de Venta"
            hint="Punto de venta utilizado para emitir el comprobante"
            v-model="cmpData.ptoVta">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-select
            :items="tiposComprobantes"
            label="Tipo de Comprobante (Número según tablas de la AFIP)"
            aria-disabled
            item-text="name"
            item-value="code"
            v-model="tipoComp">
          </v-select>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Número de Comprobante"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.nroCmp">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Importe"
            hint="Hasta 13 enteros y 2 decimales"
            aria-disabled
            v-model="cmpData.importe">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Moneda"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.moneda">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Versión"
            aria-disabled
            v-model="cmpData.ctz">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Fecha (yyyy-MM-dd)"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.tipoDocRec">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Versión"
            aria-disabled
            v-model="cmpData.nroDocRec">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Fecha (yyyy-MM-dd)"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.tipoCodAut">
          </v-text-field>
        </v-layout>
        <v-layout>
          <v-text-field
            label="Fecha (yyyy-MM-dd)"
            hint="Fecha en formato yyyy-MM-dd"
            v-model="cmpData.codAut">
          </v-text-field>
        </v-layout>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
// @ is an alias to /src
import tiposComprobantes from '@/data/tiposComprobantes.js'

export default {
  name: 'Home',
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
      tiposComprobantes: tiposComprobantes
    }
  }
}
</script>
