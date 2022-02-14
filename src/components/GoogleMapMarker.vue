<template>
    <div>
        GOOGLE MAPS MARKER TEMPLATE
    </div>
</template>
<script>
    import { chargerLogo } from '../assets/Icons.js'

    export default {
        data() {
            return {
                chargerLogo
            }
        },
        props: {
            google: {
                type: Object,
                required: true
            },
            map: {
                type: Object,
                required: true
            },
            marker: {
                type: Object,
                required: true
            },
            mapUpdated: {
                type: Object
            }
        },

        watch: {
            mapInit() {
                console.log("google prop puled into marker")
                this.initializeMarker()
            }

        },

        computed: {
            mapInit() {
                return this.mapUpdated
            }
        },

        methods: {
            initializeMarker() {
                console.log("Initialize Marker run")
                new this.google.maps.Marker({
                    position: this.marker.position,
                    marker: this.marker,
                    map: this.map
                })
            },
        },

        mounted() {
            this.initializeMarker()
            console.log("mounted run in Map Marker")
        }
    }
</script>

<style>
</style>
