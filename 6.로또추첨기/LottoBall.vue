<template>
    <div class="ball" :style="backgroundStyle">{{number}}</div>
</template>

<script>
    export default {
        name: 'LottoBall',
        props: {
            number: Number
        },
        computed: { // 새로운 값을 return
            backgroundStyle() {
                let background
                if(this.number <= 10) {
                    background = 'red'
                } else if(this.number <= 20) {
                    background = 'orange'
                } else if(this.number <= 30) {
                    background = 'yellow'
                } else if(this.number <= 40) {
                    background = 'blue'
                } else {
                    background = 'green'
                }
                return {
                    background,
                }
            }
        }
    }
</script>

<style scoped>
    .ball {
        display: inline-block;
        border: 1px solid black;
        border-radius: 25px;
        width: 40px;
        height: 40px;
        line-height: 40px;
        font-size: 20px;
        text-align: center;
        margin: 10px 20px 10px 0;
    }
</style>
