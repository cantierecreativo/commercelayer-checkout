<template>
  <v-layout row wrap>
    <v-flex xs12 px-2>
      <v-checkbox
        id="is-italian-company-checkbox"
        :label="$t('generic.is_italian_company') | capitalize"
        v-model="is_italian_company"
        color="primary"
      ></v-checkbox>
    </v-flex>
    <template v-if="is_italian_company">
      <v-flex xs6 px-2>
        <v-text-field
          id="partita-iva"
          :label="$t('generic.partita_iva') | capitalize"
          v-model="partita_iva"
          @input="handleInput()"
          @blur="handleBlur('partita_iva')"
        ></v-text-field>
      </v-flex>
      <v-flex xs6 px-2>
        <v-text-field
          id="pec"
          :label="$t('generic.pec') | capitalize"
          v-model="pec"
          @input="handleInput()"
          @blur="handleBlur('pec')"
        ></v-text-field>
      </v-flex>
      <v-flex xs6 px-2>
        <v-text-field
          id="sdi"
          :label="$t('generic.sdi') | capitalize"
          v-model="sdi"
          @input="handleInput()"
          @blur="handleBlur('sdi')"
        ></v-text-field>
      </v-flex>
    </template>
  </v-layout>
</template>

<script>
// import _ from 'lodash'
import { mapFields } from 'vuex-map-fields'

export default {
  mixins: [],
  computed: {
    ...mapFields([
      'order.is_italian_company',
      'order.partiva_iva'
    ])
  },
  methods: {
    handleInput () {
      // this.updateAddressInvalid()
    }
  }
}
</script>

<style>
</style>
