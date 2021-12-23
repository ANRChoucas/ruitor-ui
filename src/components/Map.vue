<template>
<l-map :zoom="15" :center="[46.41322, 0.219482]">
  <l-wms-tile-layer
    base-url="https://wxs.ign.fr/essentiels/geoportail/r/wms?"
    attribution="IGN"
    layer-type="base"
    name="Orthophotos"
    version="1.3.0"
    format="image/png"
    layers="ORTHOIMAGERY.ORTHOPHOTOS"
    />
  <l-layer-group
    v-if="BboxDEM"
    layerType="overlay"
    name="Zone calculable">
    <l-rectangle
      :lat-lngs="BboxDEM"
      :fill="true"
      color="#35495d"/>
  </l-layer-group>
  <l-control-layers/>
  <l-control-scale :imperial="false"/>
</l-map>
</template>

<script>
import RApi from "../axios_config.js";
  
import proj4 from "proj4";
import {
    LMap,
    LWmsTileLayer,
    LRectangle,
    LControlLayers,
    LControlScale,
    LLayerGroup
} from "@vue-leaflet/vue-leaflet";
import "leaflet/dist/leaflet.css";



export default {
    components: {
        LMap,
        LWmsTileLayer,
        LRectangle,
        LLayerGroup,
        LControlLayers,
        LControlScale
    },
    data() {
        return {
            BboxDEM: null
        }
    },
    methods: {
        toWGS84: function(coords) {
            return proj4(proj4('EPSG:2154'), proj4('EPSG:4326'), coords)
        },
        bboxToRectangle: function(bbox) {
            const p1 = bbox.slice(0,2);
            const p2 = [bbox[0], bbox[3]];
            const p3 = bbox.slice(2);
            const p4 = [bbox[2], bbox[1]];

            return [p1, p2, p3, p4]

        }
    },
    beforeCreate() {
        proj4.defs([
            [
                'EPSG:4326',
                '+title=WGS 84 (long/lat) +proj=longlat +ellps=WGS84 +datum=WGS84 +units=degrees'],
            [
                'EPSG:2154',
                '+proj=lcc +lat_1=49 +lat_2=44 +lat_0=46.5 +lon_0=3 +x_0=700000 +y_0=6600000 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs '
            ]
        ]);
    },
    created() {
        RApi.get("mnt/bbox")
            .then(response => this.BboxDEM = (
                this.bboxToRectangle(response.data)
                    .map(x => this.toWGS84(x).reverse())
            ))
            .catch(function (error) {
                console.log(error);
            })
    }
}
</script>

<style scoped>
  .leaflet-container {
  background:none;
  }
</style>
