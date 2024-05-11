<template>
<h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount" :convert="convert" :favorite="favorite"/>
    <p class="error" v-if="error != ''">{{ error }}</p>
    <p class="result-text" v-if="result != 0">{{ result }}</p>
    <Favorite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
    <div className="selectors">
        <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
        <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
    </div>
</template>

<script>
    import Input from './components/Input.vue';
    import Selector from './components/Selector.vue';
    import CryptoConvert from 'crypto-convert';
    import Favorite from './components/Favorite.vue'

    const convert = new CryptoConvert();

    export default {
        components: { Input, Selector, Favorite },
        data() {
            return {
                amount: 0,
                cryptoFirst: "",
                cryptoSecond: "",
                error: "",
                result: 0,
                favs: []
            }
        },
        methods: {
            favorite() {
               this.favs.push({
                from: this.cryptoFirst,
                to: this.cryptoSecond
               });
            },
            getFromFavs(index) {
                this.cryptoFirst = this.favs[index].from;
                this.cryptoSecond = this.favs[index].to;
            },
            changeAmount(val) {
                this.amount = val;
            },
            setCryptoFirst(val) {
                this.cryptoFirst = val;
            },
            setCryptoSecond(val) {
                this.cryptoSecond = val;
            },
            async convert() {
                this.result = "";

                if (this.amount <= 0) {
                    this.error = "Zadejte číslo vyšší než 0";
                    return;

                } else if (this.cryptoFirst === "" || this.cryptoSecond === "") {
                    this.error = "Vyberte měnu";
                    return;

                } else if (this.cryptoFirst === this.cryptoSecond) {
                    this.error = "Vyberte jinou měnu"
                    return;
                }

                this.error = "";

                await convert.ready();
                this.result = convert[this.cryptoFirst][this.cryptoSecond](this.amount);                
            }   
        }
    }
</script>

<style scoped>
   .selectors {
        display: flex;
        justify-content: space-between;
        width: 700px;
        margin: 0 auto;
    }

    .result-text {
    font-family: 'Nabla', cursive;
    font-size: 2em;
    margin: 0;
    }

    .error {
    position: relative;
    margin: 0;
    padding: 0;
    color: #aa5555;
    }
</style>