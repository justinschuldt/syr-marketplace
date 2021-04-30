<template>
  <vuetify-google-autocomplete
    id="map"
    ref="address"
    classname="form-control"
    placeholder="Please type your address"
    @placechanged="getAddressData"
  >
  </vuetify-google-autocomplete>
</template>

<script>

import Vue from 'vue'
import VuetifyGoogleAutocomplete from 'vuetify-google-autocomplete'
import * as VueGoogleMaps from 'vue2-google-maps'
const key = process.env.VUE_APP_MAP_SEARCH_KEY

Vue.use(VueGoogleMaps, {
  load: {
    key: `${key}`,
    libraries: 'places', // This is required if you use the Autocomplete plugin
  },
  // installComponents: true
})

Vue.use(VuetifyGoogleAutocomplete, {
  vueGoogleMapsCompatibility: true,
})

export default {
  components: { VuetifyGoogleAutocomplete, VueGoogleMaps },
  data () {
    return {
      address: '',
      setPlace: null,
      locations: [],
    }
  },
  computed: {
    // google: gmapApi
  },
  mounted () {
    // this.$refs.address.focus()
  },
  methods: {
    getAddressData: function (addressData, placeResultData, id) {
      this.address = addressData
      const currentPosition = {
        displayName: placeResultData.formatted_address,
        shortDisplayName: placeResultData.name,
        latitude: addressData.latitude,
        longitude: addressData.longitude,
        postcode: addressData.postal_code
      }
      // console.log(currentPosition)
      this.setPlace = currentPosition
      this.locations = currentPosition
      this.$emit('getAddressData', currentPosition)
    }
  },
}
</script>

<style lang="stylus">
.stl-places-autocomplete
  .q-select__dropdown-icon
    display: none
</style>
