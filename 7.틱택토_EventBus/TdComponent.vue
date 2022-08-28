<template>
    <td @click="onClickTd">{{cellData}}</td>
</template>

<script>
    import EventBus from './EventBus'

    export default {
        props: {
            cellData: String,
            rowIndex: Number,
            cellIndex: Number,
        },
        methods: {
            onClickTd() {
                if(this.cellData) return
                EventBus.$emit('clickTd', this.rowIndex, this.cellIndex) // emit을 이용하여 이벤트 실행
            }
        }
    }
</script>
