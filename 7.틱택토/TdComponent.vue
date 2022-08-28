<template>
    <td @click="onClickTd">{{cellData}}</td>
</template>

<script>
    export default {
        props: {
            cellData: String,
            rowIndex: Number,
            cellIndex: Number,
        },
        methods: {
            onClickTd() {
                const rootData = this.$root.$data // 상위 컴포넌트에서 data를 가져오는 방법
                this.$set(rootData.tableData[this.rowIndex], this.cellIndex, rootData.turn) // 배열의 값을 변경하는 방법
                
                let win = false
                if (rootData.tableData[this.rowIndex][0] === rootData.turn && rootData.tableData[this.rowIndex][1] === rootData.turn && rootData.tableData[this.rowIndex][2] === rootData.turn) {
                    win = true
                }
                if (rootData.tableData[0][this.cellIndex] === rootData.turn && rootData.tableData[1][this.cellIndex] === rootData.turn && rootData.tableData[2][this.cellIndex] === rootData.turn) {
                    win = true
                }
                if (rootData.tableData[0][0] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][2] === rootData.turn) {
                    win = true
                }
                if (rootData.tableData[0][2] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][0] === rootData.turn) {
                    win = true
                }

                if (win) { // 이긴 경우: 3줄 달성
                    rootData.winner = rootData.turn
                    rootData.turn = 'O'
                    rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']]
                } else { // 무승부
                    let all = true // all이 true면 무승부라는 뜻
                    rootData.tableData.forEach((row) => {
                        row.forEach((cell) => {
                            if(!cell) {
                                all = false
                            }
                        })
                    })
                    if(all) {
                        rootData.turn = 'O'
                        rootData.winner = ''
                        rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']]
                    } else {
                        rootData.turn = rootData.turn === 'O' ? 'X' : 'O'
                    }
                }
            }
        }
    }
</script>
