<template>
    <h2>Oblíbené páry</h2>
    <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
        <span>{{ el.from }}</span>
        <span>{{ el.to }}</span>
    </div>
</template>

<script>
    export default {
        props: {
            favs: {
                type: Array,
                required: true
            },
            getFromFavs: {
                type: Function,
                required: true
            }
        }
    }
</script>

<style scoped>
    div {
        display: flex;
        justify-content: space-between;
        width: 500px;
        margin: 0 auto;
        transition: all 500ms ease;
    }

    span {
        border-radius: 5px;
        padding: 10px 15px;
        background: #8c00ff;
        color: #fff;
    }

    div:hover {
        opacity: 0.7;
        transform: scale(1.1);
        cursor: pointer;
    }

    h2 {
        color: #fff;
    }
</style>