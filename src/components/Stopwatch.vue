<script>
const Stopwatch = {
    data() {
        return {
            isStarted: false,
            count: 0,
            sec: 0,
            min: 0,
            hours: 0
        }
    },
    methods: {
        startPause(event) {
            if (this.isStarted) {
                clearInterval(this.interval)
            } else {
                this.interval = setInterval(() => {
                    this.count++
                    this.sec = this.count % 60
                    this.min = Math.floor(this.count > 3600 ? this.count / 60 % 60 : this.count / 60)
                    this.hours = Math.floor(this.count / 3600)
                }, 1)
            }
            switchColor(this.isStarted, event.target)
            this.isStarted = !this.isStarted
        },
        reset(event) {
            this.isStarted = true
            this.count = 0
            this.sec = 0
            this.min = 0
            this.hours = 0
            this.startPause(event)
        }
    }
}
const switchColor = (isStarted, target) => {
    let colorToSet = ''
    if (isStarted) {
        target.parentNode.children[2].innerHTML = '&#11208;'
        colorToSet = '#9E9E9E'
    } else {
        target.innerHTML = '&#10073;&#10073;'
        colorToSet = '#FFFFFF'
    }
    let nodes = target.parentNode.children
    for (let index = 0; index < nodes.length; index++) {
        nodes[index].style.color = colorToSet;
    }
}
export default Stopwatch
</script>
<template>
    <div class="stopwatch">
        <div class="count">{{ (hours > 0 ? hours + ':' : '') + (min > 0 ? min + ':' : '') + sec }}</div>
        <hr />
        <button class="start-pause" v-on:click="startPause">&#11208;</button>
        <button class="reset" v-on:click="reset">&#9632;</button>
    </div>
</template>
<style>
.stopwatch {
    display: inline-block;
    width: 225px;
    height: 120px;
    margin: 50px;
    padding-bottom: 10px;
    background: #696969;
}

.count {
    font-family: 'Gotham Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    text-align: center;
    margin-top: 22px;
    height: 38px;
    color: #9E9E9E;
}

.start-pause {
    background-repeat: no-repeat;
    background-position-x: left;
    margin-right: 48px;
    width: 17px;
    font-size: 26px;
    background-color: #696969;
}

.reset {
    width: 20px;
    font-size: 24px;
}

hr {
    margin: 0;
    margin-bottom: 20px;
    border-color: #9E9E9E;
}
</style>