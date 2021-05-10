<template>
    <div class="image__cube">
        <div v-for="img in imgs" class="img__cube__cell">
            <img :src="img.directus_files_id.data.full_url" class="img__cube__img"/>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        imgs: Array
    }
}
</script>

<style>
.image__cube {
    width: 100%;
    margin: 40px auto 20px;
    padding: 0 10px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    justify-content: center;
}
.img__cube__cell {
    flex: 50%;
}
.img__cube__img {
    width: 100%;
    height: 100%;
    display: block;
}
/*
.img__cube__img:nth-of-type(1) {
    flex: 1 1 55%;
}
.img__cube__img:nth-of-type(2) {
    flex: 1 1 45%;
}
.img__cube__img:nth-of-type(3) {
    flex: 1 1 45%;
}
.img__cube__img:nth-of-type(4) {
    flex: 1 1 55%;
}
.img__cube__img:nth-of-type(5) {
    flex: 1 1 45%;
}
*/
    
/* ----------------------------  MEDIA QUERY ------------------------------ */
@media screen and (max-width:800px) {

} 
</style>