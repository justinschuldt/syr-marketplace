<template>
  <vue-google-autocomplete
    id="map"
    ref="address"
    classname="form-control addresssearch"
    placeholder=""
    @placechanged="getAddressData"
    @error="handleError"
  >
  </vue-google-autocomplete>
</template>

<script>

// import Vue from 'vue'
import VueGoogleAutocomplete from 'vue-google-autocomplete'
import * as VueGoogleMaps from 'vue2-google-maps'
// const key = process.env.VUE_APP_MAP_SEARCH_KEY

export default {
  components: { VueGoogleAutocomplete, VueGoogleMaps },
  data () {
    return {
      address: '',
      setPlace: null,
      locations: [],
    }
  },
  mounted () {
    // this.$refs.address.focus()
  },
  methods: {
    handleError (error) {
      console.log(error)
    },
    getAddressData: function (addressData, placeResultData, id) {
      this.address = addressData
      const currentPosition = {
        displayName: placeResultData.formatted_address,
        shortDisplayName: placeResultData.name,
        latitude: addressData.latitude,
        longitude: addressData.longitude,
        postcode: addressData.postal_code
      }
      this.setPlace = currentPosition
      this.locations = currentPosition
      this.$emit('getAddressData', currentPosition)
    }
  },
}
</script>

<style lang="stylus">
input#map {
    padding: 0;
    height: 0;
    min-height: 38px;
    line-height: 24px;
    border-width: 0 0 1px 0;
    border-color: #ccc;
    width: 100%;
}
input#map:focus {
    outline: 0!important;
    border-color: #d32f2f;
}
.addresssearch{ width: 100% }
.stl-places-autocomplete
  .q-select__dropdown-icon
    display: none
</style>
