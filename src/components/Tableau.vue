<template>
    <div class="mt-5">
        <h5>Dernière mise à jour le {{ formatDate(currency.date) }}</h5>
        <table class="table">
            <thead class="row">
                <tr class="col-12 d-flex justify-content-between">
                    <th>Montant de base --> 
                    Montant de change</th>
                </tr>
            </thead>
            <tbody class="row d-flex flex-wrap">
                <tr class="col-md-6 col-12 col-lg-4" v-bind:key="key" v-for="(value, key) in currency.rates">
                    <div class="colTab d-flex px-1 justify-content-center">
                        <td>{{ amount }} {{ currency.base }}</td>
                        <td>--></td>
                        <td>{{ value*amount|format }} <strong>{{ key }}</strong></td>
                    </div>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name:'Tableau',
        props : ['currency', 'amount', 'index'],
        methods : {
            formatDate : function(string) {
                return string.split('-').reverse().join('-');
            }
        },
        filters: {
            format (value) {
            return parseFloat(value).toFixed(2);
            }
        },
    }

</script>

<style>

</style>