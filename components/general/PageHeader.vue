<template>
    <div class="page__header">
        <h1>{{ header }}</h1>
        <p v-if="subHeader.length > 14">{{ subHeader }}</p>
    </div>
</template>

<script>
export default {
    props: {
        header: String,
        subHeader: String
    }
}
</script>

<style>
    .page__header {
        margin: 30px auto 10px;
        padding: 0 10px;
        display: block;
        width: 100%;
    }
    .page__header h1 {
        max-width: 920px;
        font-weight: 300;
        color: var(--main-text);
    }
</style>