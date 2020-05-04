<template>
    <td-component v-for="(cellData, index) in rowData" :row-index="rowIndex" :cell-data="cellData" :cell-index="index"></td-component>
</template>

<script>
    import TdComponent from "./TdComponent"
    export default {
        name: "TrComponent",
        props: {
          rowData: Array,
          rowIndex: Number
        },
        components: {
            TdComponent,
        }
    }
</script>

<style scoped>

</style>