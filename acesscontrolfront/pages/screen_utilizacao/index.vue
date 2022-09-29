<template>

    <div class="container">

      <Header />

      <div class="content">

        <div class="row-superior">

            <TitlePage />

        </div>

        <div class="row-inferior">

            <p class="subtitle">VOCÊ JÁ SABE UTILIZAR ESTA INTERFACE?</p>

            <div class="align-items-center">
            
              <button class="btn btn-sucess" v-on:click="$router.push('/screen_qrCode')">SIM</button>
              <button class="btn btn-alert" v-on:click="$router.push('/screen_tutorial')">NÃO</button>
            
            </div>

        </div>
      
      </div>
    
    </div>

</template>


<script>

export default {

  middleware: 'auth',
  name: 'screen_utilizacao',

  beforeCreate() {

    //Função para setar o tipo de redirecionamento (adm, comum e redirecionamento para logout)
    //Se for admin e possui habilidade
    if(this.$store.state.usuario.skill === true && this.$store.state.usuario.adminU === true){
      
      this.$router.push('/screen_redirectAdmin');
    
    //Se for admin
    } else if(this.$store.state.usuario.adminU === true){

      this.$router.push('/screen_admin')

    //Se não possui habilidade
    } else if(this.$store.state.usuario.skill === false){

      this.$auth.logout();
      this.$store.dispatch("SET_USER", {});
      alert("Não possui habilidade")

    //Se possui habilidade
    } else {

      //alert("Possui habilidade")

    }

  },

  data(){

    return{

     responseData: [],
     id: 0

    }

  }

}

</script>

<style lang="scss" scoped>

    @import "@/layouts/_normal_pages/Screen_Utilizacao.scss";
    @import "@/layouts/_responsividade/responsividade_grid.scss";

</style>