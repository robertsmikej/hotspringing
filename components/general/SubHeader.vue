<template>
    <h2 class="content__sub__header" v-html="text"></h2>
</template>

<script>
export default {
    props: {
        text: String
    }
}
</script>

<style>
body h2.content__sub__header {
    width: 100%;
    margin: 30px auto 0px;
    display: block;
    text-align: center;
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {

} 
</style>