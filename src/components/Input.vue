<template>
   <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Vložte částku"><br>
   <button @click="activation(); convert();" :class="isActive ? 'activate' : false">Konvertovat</button>
    <button class="favorite">Oblíbené</button>
</template>

<script>
   export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        }
    },
    data() {
        return {
            isActive: false

    }
},
    methods: {
        activation() {
            this.isActive = true;
            setTimeout(() => {this.isActive = false}, 100);
        }
    }
    
   }
</script>

<style scoped>
    input {
        border-radius: 10px;
        border: 0;
        width: 500px;
        position: relative;
        top: -50px;
        font-size: 1.2em;
        outline: none;
        padding: 10px 15px;
        background: #fafafa;
        color: #333;
    }

    button {
        position: relative;
        border-radius: 15px;
        top: -20px;
        padding: 15px 20px;
        border: 3px solid #000;
        color: #fff;
        background: #1a032d;
        text-transform: uppercase;
        cursor: pointer;
    }

    button:hover {
        scale: 1.04;
        transition: 400ms;
    }
    button.activate {
        scale: 0.9;
    }

    .favorite {
        margin-left: 20px;
    }

</style>