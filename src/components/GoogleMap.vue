<template>
  <div>
    <h1>AddGoogleMapsComponent</h1>
    <p>apiKey: {{apiKey}}</p>
    <GoogleMapLoader
        style="width: 100%; height: 300px"
        :map-config="mapConfig"
        :api-key="apiKey"
        @google-map-updated="googleMapsUpdated">
        <template v-if='updated'>
            <GoogleMapMarker
                v-for="marker in markers"
                :key="marker.id"
                :marker="marker"
                :map="map"
                :google="google"/>
        </template>
    </GoogleMapLoader>
    <template v-if='map'>
        <GoogleMapMarker
            v-for="marker in markers"
            :key="marker.id"
            :marker="marker"
            :map="map"
            :google="google"
            :mapUpdated="updated"/>
    </template>
    <p>mapConfig: {{mapConfig}}</p>
    <p>markers: {{ markers }}</p>
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
                markers: [{ id: "a", position: { lat: 51.5186395, lng: -0.2153888 }}],
                map: null,
                google: null,
                updated: {}
            }
        },

        mounted() {
            this.locateGeoLocation();
        },

        watch: {
            mapConfig: {
                handler: function() {
                    this.mapConfig.zoom
                }
            }
        },

        methods: {
            locateGeoLocation: function() {
                navigator.geolocation.getCurrentPosition(res => {
                    this.mapConfig.center = {
                        lat: res.coords.latitude,
                        lng: res.coords.longitude
                    }
                    this.updated = this.mapConfig
                    return this.mapConfig
                })
            },
            googleMapsUpdated(e) {
                console.log("googleMapsUpdated:", e)
                this.map = e.map
                console.log("this.map:", this.map)
                this.google = e.google
                console.log("this.google:", this.google)
            }
        }
    }
</script>

<style>
</style>
