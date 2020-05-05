<template>
    <td @click="onClickTd">{{cellData}}</td>
</template>

<script>
    export default {
        name: "TdComponent",
        props: {
            cellData: String,
            cellIndex: Number,
            rowIndex: Number
        },
        methods: {
            onClickTd() {
                //최상위 부모에게 한번에 접근하기 root
                console.log(this.$root.$data);
                console.log(this.$parent.$data);
                this.$root.$data.turn = this.$root.$data.turn === 'O' ? 'X' : 'O';
            }
        }
    }
</script>

<style scoped>

</style>