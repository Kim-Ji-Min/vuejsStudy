<template>
    <b-container>
        <b-row class="text-center">
            <b-col md="12">
                <h2 class="m-3 font-weight-bold">틱택토(삼목)</h2>
            </b-col>
            <b-col md="12" class="border-top p-3">
                <table-component :table-data="tableData" class="m-auto"></table-component>
                <h4 class="p-3">{{turn}}님의 턴입니다.</h4>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    import TableComponent from "./component/TableComponent";

    export default {
        name: "TicTacToe",
        data() {
            return{
                tableData: [
                    //2차원 배열
                    ['', '', ''],
                    ['', '', ''],
                    ['', '', '']
                ],
                turn: 'O',
            }
        },
        components: {
            TableComponent,
        },
        methods: {
        },
        mounted() {
        },
        beforeDestroy() {
        },
        watch: {
        }
    }
</script>

<style>
    table{
        border-collapse: collapse;
    }
    td{
        border: 1px solid #ccc;
        width: 100px;
        height: 100px;
        text-align: center;
    }
</style>
