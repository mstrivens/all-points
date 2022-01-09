<template>
  <div>
    <h1>AddGoogleMapsComponent</h1>
    <p>apiKey: {{apiKey}}</p>
    <vue-google-maps
        style="width: 100%; height: 300px"
        :map-config="mapConfig"
        :api-key="apiKey">
    </vue-google-maps>
    <p>mapConfig: {{mapConfig}}</p>
  </div>
</template>

<script>
    import VueGoogleMaps from "@point-hub/vue-google-maps";

    export default {
        components: {
            VueGoogleMaps
        },

        data() {
            return {
                apiKey: process.env.VUE_APP_API_KEY,
                mapConfig: {
                    zoom: 16,
                    center: {
                        lat: -7,
                        lng: 112
                    }
                },
                locationMarkers: [],
                locPlaces: [],
                existingPlace: null
            }
        },

        mounted() {
            this.locateGeoLocation();
        },

        watch: {
            locateGeoLocation() {
                this.mapConfig.zoom
            }
        },

        methods: {
            locateGeoLocation: function() {
                navigator.geolocation.getCurrentPosition(res => {
                    this.mapConfig.center = {
                        lat: res.coords.latitude,
                        lng: res.coords.longitude
                    }
                    console.log(this.mapConfig.center)
                })
            },
        }
    }
</script>

<style>
</style>
