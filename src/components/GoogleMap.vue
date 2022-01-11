<template>
  <div>
    <h1>AddGoogleMapsComponent</h1>
    <p>apiKey: {{apiKey}}</p>
    <GoogleMapLoader
        style="width: 100%; height: 300px"
        :map-config="mapConfig"
        :api-key="apiKey">
        <GoogleMapMarker
            v-for="marker in markers"
            :key="marker.id"
            :marker="marker"
            :google="google"
            :map="map"/>
    </GoogleMapLoader>
    <p>mapConfig: {{mapConfig}}</p>
  </div>
</template>

<script>
    import GoogleMapLoader from "./GoogleMapLoader.vue";
    import GoogleMapMarker from "./GoogleMapMarker.vue";

    export default {
        components: {
            GoogleMapLoader,
            GoogleMapMarker
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
                existingPlace: null,
                markers: [{ id: "a", position: { lat: -51.51, lng: -0.2}}]
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
