<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="cryptoNow === 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="setCrypto('ETH')" :class="cryptoNow === 'ETH' ? 'active' : ''">ETH</li>
        <li @click="setCrypto('USD')" :class="cryptoNow === 'USD' ? 'active' : ''">USD</li>
    </ul>
</template>

<script>
    export default {
        props: {
            setCrypto: {
                type: Function,
                required: true
            },
            cryptoNow: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        width: 200px;
        padding: 0;
        border-radius: 13px;
        border: 3px solid #000;
    }

    li {
        display: block;
        background: #1A032d;
        color: #fff;
        padding: 20px 0;
    }

    li:hover, li.active {
        border-radius: 13px;
        background: #4f157e;
        cursor: pointer;
    }

</style>