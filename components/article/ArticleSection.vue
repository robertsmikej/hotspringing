<template>
    <div class="site__section article__section">
        <nuxt-link v-for="(cell, index) in cells" :key="index" :to="'/articles/' + cell.condensed_title"  class="grid__cell article__trip__cell">
            <div v-if="cell.article_type !== null" :data-article-type="cell.article_type.replace(/ /g,'-').toLowerCase()" class="article__callout__container">
                <h6 class="article__callout">{{ cell.article_type }}</h6>
            </div>
            <div class="grid__image__container">
                <img :src="'https://www.hotspringing.com/directus/public/thumbnail/_/500/333/crop/good/' + cell.article_thumbnail.filename" alt="" class="grid__image">
            </div>
            <div class="grid__text article__cell__text">
                <h3 v-if="cell.article_title_second_line !== null" class="article__trip__cell__header">{{ cell.article_title + " " + cell.article_title_second_line }}</h3>
                <h3 v-else class="article__trip__cell__header">{{ cell.article_title }}</h3>
                
                <p class="grid__description__text">{{ cell.short_description }}</p>
            </div>
        </nuxt-link>
    </div>
</template>

<script>
export default {
    props: {
        cells: Object
    }
}
</script>

<style>
.article__section {
    width: 100%;
    max-width: 1500px;
    height: auto;
    margin: 6px auto 20px;
    padding: 0 32px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: center;
    justify-content: flex-start;
    box-sizing: border-box;
}
.article__section .article__trip__cell {
    flex: 0 1 25%;
    padding: 0 8px;
    height: auto;
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
.article__section .article__cell__text {
    padding-top: 8px;
}
.article__callout {
    padding: 14px 5px;
    font-size: 15px;
    line-height: 15px;
    font-weight: 300;
    letter-spacing: .6px;
/*    text-transform: uppercase;*/
}
[data-article-type="tips-&-tricks"] {
    background-color: var(--dark-teal);
}
[data-article-type="trip-report"] {
    background-color: var(--dark-grey);
}
.article__section p {
    font-weight: 300;
    line-height: 21px;
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:1200px) {
    .article__section {
        padding: 0 10px;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {
    .article__section .article__trip__cell {
        flex: 0 1 50%;
        padding: 0 4px;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:600px) {
    .article__section {
        padding: 0 4px;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:500px) {
    .article__section .article__trip__cell {
        flex: 0 1 50%;
    }
    .article__section .grid__description__text {
        margin-top: 0;
    }
}  
</style>