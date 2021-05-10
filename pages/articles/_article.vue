<template>
    <div>
        <Hero :hero="articles[$route.params.article]"/>
        <div class="article__content">
        
            <PageHeader :header="articles[$route.params.article].intro_header || ''" :subHeader="articles[$route.params.article].intro_text || ''"/>
            
            <h4 v-if="articles[$route.params.article].published_date !== null" class="publish__date">Publised On: {{ articles[$route.params.article].published_date }}</h4>

            <TextImgContentCell :text="articles[$route.params.article].opening_text || ''" :image="articles[$route.params.article].article_image_1" :imageAlt="altText(articles[$route.params.article].article_image_1)" :caption="altText(articles[$route.params.article].article_image_1)"/>
            
            <SubHeader v-if="articles[$route.params.article].content_sub_header !== 'null'" :text="articles[$route.params.article].content_sub_header"/>
           
            <TextContentCell v-if="articles[$route.params.article].text_body_1 !== 'null'" :text="articles[$route.params.article].text_body_1"/>
            
            <ImgCube v-if="articles[$route.params.article].article_images_2.length > 0" :imgs="articles[$route.params.article].article_images_2"/>

            <TextContentCell v-if="articles[$route.params.article].text_body_2 !== 'null'" :text="articles[$route.params.article].text_body_2"/>
            
            <TextImgContentCell :text="articles[$route.params.article].text_body_3" :image="articles[$route.params.article].article_image_3" :imageAlt="altText(articles[$route.params.article].article_image_3)"/>

            <TextContentCell v-if="articles[$route.params.article].ending_text !== 'null'" :text="articles[$route.params.article].ending_text"/>
            
        </div>

    </div>
</template>

<!--
        <div class="map__collapse all__side" :class="{collapsed: isCollapsed}">
            <div class="map__collapse__inner">
                <MapContainerFull :mapData="map" :marks="pins(springs)"/>
            </div>
            <div class="map__collapse__expand__div" @click="mapCollapse">
                <div class="map__collapse__expand" :class="{collapseTurn: isCollapsed}"/>
            </div>
        </div>
-->
<!--        <Comments :data="$route.params.name"/>-->

<script>
    import Hero from '~/components/hero/Hero.vue';
    import PageHeader from '~/components/general/PageHeader.vue';
    import TextImgContentCell from '~/components/general/TextImgContentCell.vue';
    import TextContentCell from '~/components/general/TextContentCell.vue';
    import SubHeader from '~/components/general/SubHeader.vue';
    import SectionHeader from '~/components/general/SectionHeader.vue';
    import ImgCube from '~/components/general/ImgCube.vue';
    import ArticleSection from '~/components/article/ArticleSection.vue';
    import MapContainerFull from '~/components/maps/MapContainerFull.vue';
    
    export default {
        components: {
            Hero,
            PageHeader,
            TextImgContentCell,
            TextContentCell,
            SubHeader,
            SectionHeader,
            ImgCube,
            ArticleSection,
            MapContainerFull
        },
        computed: {
            articles: function () {
                return this.$store.state.articles
            }
        },
        head () {
            return {
                title: this.$store.state.articles[this.$route.params.article].article_title + " " + this.$store.state.articles[this.$route.params.article].article_title_second_line + " | HotSpringing.com",
                meta: [
                    {hid: 'description', name: 'description', content: this.$store.state.articles[this.$route.params.article].short_description}
                ]
            }
        },
        methods: {
            altText: function (text) {
                if (text !== null) {
                    if (text.metadata !== null && text.metadata.title !== null) {
                        return text.metadata.title;
                    }
                } else {
                    return;
                }
            }
        }
    }
</script>

<style>
.article__content {
    max-width: 1000px;
    width: 100%;
    margin: 0 auto 50px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    justify-content: center;
    padding: 0;
}
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
.publish__date {
    margin-bottom: 20px;
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {
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