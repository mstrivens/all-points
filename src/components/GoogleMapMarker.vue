<template>
    <div>
        {{ chargerLogo }}
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
            }
        },

        mounted() {
            console.log("Created starting in Map MArker")
            new this.google.maps.Marker({
                position: this.marker.position,
                marker: this.marker,
                map: this.map,
                icon: this.chargerLogo,
            })
            console.log("mounted run in Map Marker")
        }
    }
</script>

<style>
</style>
