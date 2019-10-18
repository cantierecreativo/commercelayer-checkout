<template>
  <v-layout row wrap>
    <v-flex xs12 px-2 v-if="requires_billing_info">
      <v-checkbox
        id="is-italian-company-checkbox"
        :label="$t('generic.is_italian_company') | capitalize"
        v-model="is_italian_company"
        @change="handleChange()"
      ></v-checkbox>
    </v-flex>
    <template v-if="is_italian_company">
      <v-flex xs6 px-2>
        <v-text-field
          id="partita-iva"
          :label="$t('generic.partita_iva') | capitalize"
          v-model="partita_iva"
          :error-messages="errorMessages('partita_iva')"
          @input="handleInput()"
          @blur="handleBlur('partita_iva')"
        ></v-text-field>
      </v-flex>
      <v-flex xs6 px-2>
        <v-text-field
          id="sdi"
          :label="$t('generic.sdi') | capitalize"
          v-model="sdi"
          :error-messages="errorMessages('sdi')"
          @input="handleInput()"
          @blur="handleBlur('sdi')"
        ></v-text-field>
      </v-flex>
      <v-flex xs12 px-2>
        <v-text-field
          id="pec"
          :label="$t('generic.pec') | capitalize"
          v-model="pec"
          :error-messages="errorMessages('pec')"
          @input="handleInput()"
          @blur="handleBlur('pec')"
        ></v-text-field>
      </v-flex>
    </template>
  </v-layout>
</template>

<script>
import { mapFields } from 'vuex-map-fields'
import { required, requiredIf } from 'vuelidate/lib/validators'

export default {
  computed: {
    ...mapFields([
      'validations.invalid_billing_address',
      'order.requires_billing_info',
      'order.is_italian_company',
      'order.partita_iva',
      'order.pec',
      'order.sdi'
    ])
  },
  validations: {
    partita_iva: { required: requiredIf(function (model) {
      return this.is_italian_company
    }) },
    pec: { required: requiredIf(function (model) {
      return this.is_italian_company
    }) },
    sdi: { required: requiredIf(function (model) {
      return this.is_italian_company
    }) }
  },
  methods: {
    handleChange () {
      this.updateAddressInvalid()
    },
    handleInput () {
      this.updateAddressInvalid()
    },
    handleBlur (fieldName) {
      this.$v[fieldName].$touch()
    },
    updateAddressInvalid () {
      this.invalid_billing_address = 
        this.is_italian_company && this.$v.$invalid
    },
    errorMessages (fieldName) {
      const errors = []
      if (!this.$v[fieldName].$dirty) return errors
      !this.$v[fieldName].required && errors.push("Can't be blank")
      return errors
    }
  }
}
</script>

<style>
</style>
