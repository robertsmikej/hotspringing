<template>
    <div class="article__img__text__cell">
        <div class="article__inner__content" v-html="text"></div>
        <div class="article__inner__content">
            <div class="article__content__image__div">
               
                <img v-if="image !== null" :src="image.data.thumbnails[4].url" :alt="imageAlt" class="article__content__image">
                <p v-if="caption !== null" class="article__content__image__caption">{{ caption }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        text: String,
        caption: String,
        image: Object,
        imageAlt: String
    }
}
</script>

<style>
.article__inner__content {
    padding: 0 10px;
    margin: 20px 0 0;
    display: flex;
  	flex-direction: column;
   	flex-wrap: wrap;
   	align-content: flex-start;
   	justify-content: flex-start;
}
.article__content h2 {
    margin: 0 0 20px;
}
.article__content p {
    line-height: 28px;
    font-size: 18px;
    margin: 6px 0 0;
}
.article__img__text__cell {
    max-width: 1000px;
    width: 100%;
    margin: 0 auto;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    justify-content: center;
}
.article__img__text__cell:nth-of-type(odd) .article__inner__content:nth-of-type(1) {
    width: 50%;
    order: 2;
}
.article__img__text__cell:nth-of-type(odd) .article__inner__content:nth-of-type(2) {
    width: 50%;
    order: 1;
}
.article__img__text__cell:nth-of-type(even) .article__inner__content:nth-of-type(1) {
    width: 50%;
}
.article__img__text__cell:nth-of-type(even) .article__inner__content:nth-of-type(2) {
    width: 50%;
}
.article__content__image__div {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: center;
    justify-content: center;
    overflow: hidden;
}
.article__content__image {
    max-width: 100%;
    align-self: center;
}
p.article__content__image__caption {
    width: 100%;
    margin: 5px 0;
    text-align: center;
    font-size: 12px;
    line-height: 12px;
    font-weight: 400;
    text-transform: capitalize;
}   
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {
    .article__img__text__cell:nth-of-type(1) .article__inner__content:nth-of-type(1) {
        width: 100%;
    }
    .article__img__text__cell:nth-of-type(1) .article__inner__content:nth-of-type(2) {
        width: 100%;
    }
    .article__img__text__cell:nth-of-type(2) .article__inner__content:nth-of-type(1) {
        width: 100%;
        order: 1;
    }
    .article__img__text__cell:nth-of-type(2) .article__inner__content:nth-of-type(2) {
        width: 100%;
        order: 2;
    }
    .article__content h2 {
        text-align: center;
    }
    .article__content__image {
        width: 100%;
        max-width: 300px;
        margin-left: auto;
        margin-right: auto;
        display: block;
    }
}
</style>