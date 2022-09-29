<template>

    <div class="container">

        <Header/>

        <div class="view-center">

            <p class="text-info">A máquina em utilização. A liberação foi feita com sucesso, bom trabalho! </p>

            <button class="btn_off">
                <p class="text-btn-off" v-on:click="turnOffMachine()">Desligar</p>
            </button>

        </div>

    </div>

</template>

<script>

    export default{

        name: "screen_standby",

        data(){

            return{
                dataMachine: [],
            }

        },

        methods:{

            updateMachinesFields: function(){

                const date = new Date();
                let bodyMachine = [];

                let hour = date.getHours();          
                let min = date.getMinutes();        
                let seg = date.getSeconds();

                let fullHour = hour + ":" + min + ":" + seg;

                fullHour.toString(); 

                bodyUpdate = {
                    hourFinish: fullHour
                },  

                this.$axios.patch(this.$store.state.BASE_URL + "/releasemachines/" + this.$store.state.idrealesed + '/', bodyUpdate).then((response) => {
                   
                    console.log(response)
                    this.$router.push("/screen_home")

                }).catch((error) =>{
                    console.log(error)
                })

            },

            turnOffMachine: function(){

                let bodyMachine = {
                    name: this.$store.state.machine.name,
                    description: this.$store.state.machine.description,
                    status: false,
                    ipaddress: this.$store.state.machine.ipaddress,
                    statusMaint: this.$store.state.machine.statusMaint
                }

                this.$axios.put(this.$store.state.BASE_URL + "/machines/" + this.$store.state.idmachine + "/", bodyMachine).then((response) => {

                    this.updateMachinesFields();

                }).catch((error) => {

                    console.log(error);

                })

            },

        }

    }

</script>

<style lang="scss" scoped>

    @import "@/layouts/_normal_pages/Screen_Standby.scss";
    @import "@/layouts/_responsividade/responsividade_grid.scss";

</style>