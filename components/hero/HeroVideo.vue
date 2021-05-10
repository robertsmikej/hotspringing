<template>
    <video playsinline autoplay muted loop class="hero__header__video">
        <source :src="video.data.full_url" type="video/mp4">
    </video>
</template>

<script>
export default {
    props: {
        video: Object
    }
}
</script>

<style>
.hero__video__img__container video {
    max-width: 2300px;
    max-height: 700px;
    width: 100%;
    height: auto;
    -o-object-fit: cover;
    object-fit: cover;
    -ms-flex-item-align: center;
    align-self: center;
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:1000px) {
    .hero__video__img__container video {
        min-height: 400px;
    }
}
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:600px) {
    .hero__video__img__container video {
        min-height: 65vh;
    }
}
</style>