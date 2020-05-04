<template>
    <b-container>
        <b-row class="text-center">
            <b-col md="12">
                <h2 class="m-3 font-weight-bold">틱택토(삼목)</h2>
            </b-col>
            <b-col md="12">
                <table-component :table-data="tableData"></table-component>
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

<style scoped>
</style>
