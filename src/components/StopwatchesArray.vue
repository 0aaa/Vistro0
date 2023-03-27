<script>
import Stopwatch from './Stopwatch.vue'
const Stopwatches = {
    data() {
        return {
            cnt: 0,
            stopwatchesArr: [
                { count: 0, iden: 0 },
                { count: 0, iden: 1 },
                { count: 0, iden: 2 }
            ]
        }
    },
    components: {
        Stopwatch
    },
    methods: {
        add() {
            let iden = this.cnt++
            this.stopwatchesArr.push({ count: 0, iden: iden })
        }
    }
}
export default Stopwatches
</script>
<template>
    <Stopwatch v-for="i in stopwatchesArr" :iden="i.iden" />
    <button id="add" v-on:click="add">+</button>
</template>
<style>
#add {
    position: relative;
    top: -30px;
    width: 225px;
    height: 130px;
    margin: 50px;
}

@media screen and (max-width: 1024px) {
    template {
        width: 1024px;
    }
}

@media screen and (max-width: 768px) {
    template {
        width: 768px;
    }
}

@media screen and (max-width: 320px) {
    template {
        width: 320px;
    }
}
</style>