<template>
    <GmapMap :center="center" :zoom="zoom" :map-type-id="mapType" :options="mapStyle">
        <gmap-info-window :options="infoOptions" :position="infoPosition" :opened="infoOpened" @closeclick="infoOpened=false">
            <div class="info__windows">
                <nuxt-link class="info__window__name" :to="'/hotsprings/' + springCondName">{{ springName }}</nuxt-link>
                <div class="rating">
                    <h3>Our Rating: </h3>
                    <div :data-rating="springRating" class='rating__star__container'>
                        <div class="rating__color" :style="{right: springMove + '%'}"></div>
                        <img alt="Star Rating Block" src="https://www.hotspringing.com/directus/public/uploads/_/originals/hollowStars.png">
                    </div>
                </div>
                <h3>Walking Distance: {{ springWalkingDist }}</h3>
                <h3>Parking Cost: ${{ springParkingCost }}</h3>
                <h3>Accessable Seasons: {{ springSeasons }}</h3>
                <div class="info__window__description" v-html="springDescription"/>
                <a class="info__directions__link" :href='"https://www.google.com/maps/dir/?api=1&destination=" + springLatitude + "," + springLongitude' target='_blank'>Get Directions</a>
            </div>
        </gmap-info-window>
        <GmapMarker v-for="(item, index) in markers" :key="index" :position="getPosition(item)" :clickable="true" @click="toggleInfo(item, index)"/>
    </GmapMap>
</template>

<script>
//    import MapInfoWindow from "~/components/maps/MapInfoWindow.vue";
    
    let mapStyles = [ //MAP STYLES
        {
            "featureType": "administrative",
            "elementType": "labels.text.fill",
            "stylers": [
                {
                    "color": "#232323"
                }
            ]
        },
        {
            "featureType": "administrative",
            "elementType": "geometry.fill",
            "stylers": [
                {
                    "visibility": "on"
                }
            ]
        },
        {
            "featureType": "landscape",
            "elementType": "all",
            "stylers": [
                {
                    "color": "#f2f2f2"
                }
            ]
        },
        {
            "featureType": "poi.park",
            "elementType": "all",
            "stylers": [
                {
                    "visibility": "off"
                }
            ]
        },

        {
            "featureType": "road.highway",
            "elementType": "labels.text",
            "stylers": [
                {
                    "visibility": "on"
                },
                {
                    "color": "grey"
                }
            ]
        },
        {
            "featureType": "road.highway",
            "elementType": "geometry",
            "stylers": [
                {
                    "visibility": "simplified"
                },
                {
                    "color": "#3B4541"
                }
            ]
        },
        {
            "featureType": "road.highway",
            "elementType": "labels.icon",
            "stylers": [
                {
                    "visibility": "simplified"
                }
            ]
        },
        {
            "featureType": "road",
            "elementType": "labels",
            "stylers": [
                {
                    "visibility": "on"
                }
            ]
        },
        {
            "featureType": "transit",
            "elementType": "all",
            "stylers": [
                {
                    "visibility": "off"
                }
            ]
        },
        {
            "featureType": "water",
            "elementType": "all",
            "stylers": [
                {
                    "color": "#6DCDEC"
                },
                {
                    "visibility": "on"
                }
            ]
        }
    ];
    export default {
        props: {
            mapData: Object,
            marks: Array
        },
        data() {
            return {
                center: { lat: parseFloat(this.mapData.center.latitude), lng: parseFloat(this.mapData.center.longitude) },
                zoom: 6,
                mapType: "roadmap",
                mapStyle: {styles: mapStyles},
                markers: this.marks,
                infoPosition: null,
                infoContent: null,
                springName: null,
                springCondName: null,
                springRating: null,
                springWalkingDist: null,
                springParkingCost: null,
                springSeasons: null,
                springDescription: null, 
                springLatitude: null,
                springLongitude: null,
                springMove: null,
                infoOpened: false,
                infoCurrentKey: null,
                infoOptions: {
                    pixelOffset: {
                        width: 0,
                        height: -35
                    }
                }
            };
        },
        methods: {
            getPosition: function(marker) {
                return {
                    lat: marker.position.lat,
                    lng:  marker.position.lng
                }
            },
            toggleInfo: function(marker, key) {
                var s = marker.details;
                this.infoPosition = this.getPosition(marker);
                console.log(marker);
                this.springName = marker.details.name;
                this.springCondName = marker.details.condName;
                this.springRating = marker.details.rating;
                this.springWalkingDist = marker.details.walkingDist;
                this.springParkingCost = marker.details.parkingCost;
                this.springSeasons = marker.details.seasons;
                this.springDescription = marker.details.description;
                this.springLatitude = marker.details.latitude;
                this.springLongitude = marker.details.longitude;
                this.springMove = marker.details.rating / 100 * (80 * -1);
                if (this.infoCurrentKey == key) {
                    this.infoOpened = !this.infoOpened;
                } else {
                    this.infoOpened = true;
                    this.infoCurrentKey = key;
                }
            }
        }
    }
</script>

<style>

.vue-map-container, .vue-map-container .vue-map {
	width: 100%;
    margin-bottom: 0px;
    min-height: 500px;
}
.map__collapse__inner .vue-map-container, .map__collapse__inner .vue-map-container .vue-map {
	width: 100%;
    margin-bottom: 0px;
    height: 55vh;
    min-height: 55vh;
    max-height: 55vh;
    transition: all .8s;
}
body .collapsed .vue-map-container, body .collapsed .vue-map-container .vue-map {
	width: 100%;
    margin-bottom: 0px;
    height: 20vh;
    min-height: 20vh;
    max-height: 20vh;
}
.map__collapse {
    max-height: 55vh;
    min-height: 55vh;
    width: 100%;
    transition: all .8s;
    margin-bottom: 40px;
}
body .collapsed {
    max-height: 20vh;
    min-height: 20vh;
}
.map__collapse__inner {
    overflow: hidden;
    max-height: inherit;
}
.map__collapse__expand__div {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 5px;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    border-bottom: 3px solid var(--main-text);
}
.map__collapse__expand {
    width: 0;
    height: 0;
    position: relative;
    border-left: 40px solid transparent;
    border-right: 40px solid transparent;
    border-top: 36px solid var(--main-text);
    cursor: pointer;
    left: 50%;
    bottom: 16px;
    animation: grab-attention 2s;
    transition: all .4s;
    transform: rotateX(180deg) translate(-50%, 0);
    transform-origin: center center;
}
.collapseTurn {
    transform: rotateX(0deg) translate(-50%, 0);
    bottom: -20px;
}
@keyframes grab-attention {
    0% {
        transform: scale(1);
        transform: rotate(0deg);
    }
    50% {
        transform: scale(2);
        transform: rotate(0deg);
    }
    100% {
        transform: scale(1);
        transform: rotate(0deg);
    }
}
.map__collapse__expand::after {
    
    content: "Close";
    position: absolute;
    bottom: 0;
    left: 50%;
    color: #FFF;
    font-size: 10px;
    transform: rotateX(180deg) translate(-50%, 180%);
}
.collapseTurn.map__collapse__expand::after {
    content: "Expand";
    transform: rotateX(0deg) translate(-50%, -180%);
}
.info__windows {
    max-width: 300px;
}
.info__window__name {
    text-decoration: none;
    font-family: var(--font-headers);
    font-size: 20px;
    line-height: 20px;
    font-weight: 400;
	margin: 0 0 4px 0;
	padding: 0;
    color: var(--dark-teal);
    text-align: left;
	text-transform: uppercase;
}
.rating h3 {
    margin-bottom: 0;
}
.info__directions__link {
    font-size: 16px;
    font-weight: 400;
    margin: 5px 0 0;
}

/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {
    .map__collapse__inner .vue-map-container, .map__collapse__inner .vue-map-container .vue-map, .map__collapse {
        height: 80vh;
        min-height: 80vh;
        max-height: 80vh;
    }
}
</style>