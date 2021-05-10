<template>
    <div class="article__inner__content" v-html="text"></div>
</template>

<script>
export default {
    props: {
        text: String
    }
}
</script>

<style>

/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {

} 
</style>