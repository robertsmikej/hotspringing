<template>
    <div class="site__section grid__section">
        <nuxt-link v-for="(cell, index) in cells" :key="index" :to="'/hotsprings/' + cell.condensed_page_name"  class="grid__cell">
            <div class="grid__cell__inner__wrap">
                <div class="grid__image__container">
                    <img :src="'https://www.hotspringing.com/directus/public/thumbnail/_/300/200/crop/good/' + cell.thumbnail_image.filename" alt="" class="grid__image">
                </div>
                <div class="grid__text">
                    <div class="grid__commercial__surround">
                        <h6 v-if="cell.commercial" class="grid__commericial__callout">Commercial</h6>
                        <h6 v-else class="grid__natural__callout">Natural</h6>
                        <h4>{{ cell.nearest_town }}</h4>
                    </div>
                    <h3>{{ cell.name }}</h3>
                    <div class="rating">
                        <h4>Our Rating: </h4>
                        <div class="rating__star__container" :data-rating=cell.rating>
                            <div class="rating__color"></div>
                            <img alt="Rating Star" src="https://www.hotspringing.com/directus/public/uploads/_/originals/hollowStars.png">
                        </div>
                    </div>
                    
                    <div class="grid__description__text" v-html="cell.description"></div>
                </div>
            </div>
        </nuxt-link>
    </div>
</template>

<script>
export default {
    props: {
        cells: Object
    },
    mounted() {
        var ratingContainers = document.getElementsByClassName('rating__star__container'),
            i;
        for (i = 0; i < ratingContainers.length; i += 1) {
            var container = ratingContainers[i],
                rating = container.getAttribute('data-rating'),
                move = rating / 100 * (80 * -1);
            container.querySelector('.rating__color').style.right = move + "px";
        }
    }
}
</script>

<style>
.grid__section {
	width: 100%;
	max-width: 1500px;
	height: auto;
 	margin: 6px auto 20px;
  	padding: 0 32px;
  	display: -webkit-box;
  	display: -ms-flexbox;
  	display: flex;
 	-webkit-box-orient: horizontal;
 	-webkit-box-direction: normal;
 	-ms-flex-direction: row;
 	flex-direction: row;
  	-ms-flex-wrap: wrap;
  	flex-wrap: wrap;
  	-ms-flex-line-pack: center;
  	align-content: center;
  	justify-content: flex-start;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
.grid__section::-webkit-scrollbar {
	display: none;
}
.grid__cell {
    flex: 0 1 16%;
 	margin: 6px 0 10px;
  	padding: 0;
  	display: -webkit-box;
  	display: -ms-flexbox;
  	display: flex;
 	-webkit-box-orient: vertical;
 	-webkit-box-direction: normal;
 	-ms-flex-direction: column;
 	flex-direction: column;
  	-ms-flex-wrap: nowrap;
  	flex-wrap: nowrap;
  	-ms-flex-line-pack: center;
  	align-content: center;
	cursor: pointer;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
.grid__cell__inner__wrap {
	padding: 0 8px;
	height: 100%;
    overflow: hidden;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-direction: column;
    flex-direction: column;
}
.grid__image__container {
	width: 100%;
}
.grid__image {
    width: 100%;
    display: block;
}
.grid__text {
	position: relative;
 	margin: 0;
    -webkit-box-flex: 1;
    -ms-flex: 1;
    flex: 1;
  	padding: 4px 0px;
  	display: -webkit-box;
  	display: -ms-flexbox;
  	display: flex;
 	-webkit-box-orient: vertical;
 	-webkit-box-direction: normal;
 	-ms-flex-direction: column;
 	flex-direction: column;
  	-ms-flex-wrap: nowrap;
  	flex-wrap: nowrap;
  	-ms-flex-line-pack: center;
  	align-content: center;
  	-webkit-box-pack: start;
  	-ms-flex-pack: start;
  	justify-content: flex-start;
    background-color: #FFF;
}
.grid__commercial__surround {
    margin: 0 0 5px;
    align-self: flex-start;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
}
.grid__commericial__callout, .grid__natural__callout {
    padding: 3px 6px;
    display: block;
    font-size: 11px;
    line-height: 11px;
    border-radius: 3px;
    font-weight: 300;
    text-transform: uppercase;
    margin-right: 4px;
    margin-top: 3px;
}
.grid__commericial__callout {
    background-color: var(--dark-teal);
}
.grid__natural__callout {
    background-color: var(--green);
}
.grid__commercial__surround h4 {
    font-size: 15px;
    line-height: 15px;
    margin: 4px 0 0;
    align-self: center;
    white-space: nowrap;
}
.grid__description__text {
    margin-top: 0px;
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:1200px) {
	.grid__section {
		padding: 0 8px;
        margin-bottom: 0;
	}
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:1100px) {  
    .grid__cell {
        flex: 0 1 33.33333%;
        margin: 6px 0 22px;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {  
    .grid__cell {
        margin: 10px 0px;
        padding: 0;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:600px) {
    .grid__section {
		padding: 0 5px;
	}
    .grid__commericial__callout, .grid__natural__callout {
        padding: 2px 4px;
    }
    .grid__commercial__surround {
        flex-wrap: wrap;
    }
    .grid__cell:nth-of-type(even) .grid__cell__inner__wrap {
        padding: 0 3px 0 3px;
    }
    .grid__cell:nth-of-type(odd) .grid__cell__inner__wrap {
        padding: 0 3px 0 3px;
    }
    .grid__cell {
        flex: 0 1 50%;
        margin: 8px 0px;
    }
}
</style>