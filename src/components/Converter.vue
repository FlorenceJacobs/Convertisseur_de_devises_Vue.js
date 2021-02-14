<template>
    <div class="container mt-5" id="app">
        <h1>Convertisseur de monnaies</h1>
        <form class="flex row mt-5">
            <div class="col-6 col-md-3">
                <label for="montant" class="h3">Montant</label>
                <input type="number" class="form-control" id="montant" v-model="amount" />
            </div>
            <div class="col-6 col-md-3">
                <label for="devise" class="h3">Devise</label>
                <select class="form-control" id="devise" @change="getBase">
                    <option :value="code" :key="keytest" v-for="(code, keytest) in testCode">{{ code }}</option>
                </select>
            </div>
        </form>
        <tableau v-bind:currency="currency" v-bind:amount="amount"></tableau> 
    </div>
</template>

<script>
    import axios from 'axios'
    import Tableau from './Tableau'
    export default {
        name:'Converter',
        data(){
            return {
                codesPays: [
                    {abrev: 'EUR', nomComplet: 'EUR : Euro'},
                ],
                testCode : [],
                amount: 1,
                currency: {},
                date: "2021-02-19",
            }
        },

        methods: {
            calculRate (base) {
            axios
                .get('https://api.exchangeratesapi.io/latest', {
                    params: {
                    base: base
                    }
                })
                .then((reponse) => {
                    this.currency = reponse.data;
                    console.log(this.currency);
                    this.testCode = Object.keys(reponse.data.rates).filter(code => code !== base);
                    console.log(this.testCode);
                })
                .catch((error) => {
                    console.log(error);
                });
            },
            getBase (event) {
                this.calculRate(event.target.value);
            },
        },
        mounted () {
            this.calculRate(this.codesPays[0].value);
        },
        components:{
            'tableau' : Tableau,
        }
    };

</script>

<style>

</style>
