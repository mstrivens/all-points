<template>
  <div>
    <div id="map" style="width:100%;height:100%"></div>
  </div>
</template>

<script>
import GoogleMapsApi from "@point-hub/google-maps-api";

export default {
    props: {
        mapConfig: {
            type: Object,
            required: true
        },
        apiKey: {
            type: String,
            required: true
        },
        libraries: {
            type: Array,
            required: false
        }
    },
    emits: ["google-map-updated"],
    data() {
        return {
            google: null,
            map: null,
            config: this.mapConfig.center.lat
        };
    },
    mounted() {
        GoogleMapsApi({
            libraries: this.libraries,
            apiKey: this.apiKey
        }).then(google => {
            this.google = google;
            this.initializeMap();
            // this.emitGoogleData()
            // this.emitMapData()
        });
    },
    watch: {
        mapConfig: {
            handler: function() {
                console.log("mapConfig changed in MapLoader")
                this.initializeMap();
            },
            deep: true
        }
    },
    methods: {
        initializeMap() {
            const mapContainer = this.$el.querySelector("#map");
            const { Map } = this.google.maps;
            this.Newmap = new Map(mapContainer, this.mapConfig);
            this.$emit("google-map-updated", {
                map: this.Newmap,
                google: this.google
            });
        },
    }
};
</script>
