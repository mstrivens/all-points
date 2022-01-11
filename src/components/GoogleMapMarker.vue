<template>
    <div>
        <img="chargerLogo"/>
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
            new this.google.maps.Marker({
                position: this.marker.position,
                marker: this.marker,
                map: this.map,
            })
        }
    }
</script>

<style>
</style>
