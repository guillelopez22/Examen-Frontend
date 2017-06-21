<template>

      <router-view ></router-view><!--Aqui se renderiza lo de cada ruta-->
    
</template>

<script>
import baseUrl from '../config'
export default {
  name: 'app',
  methods:{
    logout(){
      this.$http.get(`${baseUrl.uri}/v1/logout`).then((response)=>{
        this.$router.push('/');
      });
    }
  }
}
</script>

<style scoped>
  .themeBiblioteca{
    background-color: #D1D1D1;
  }
  .nav-extended{
    padding-left: 100px;
    padding-right: 100px;
    background-color: #4C1B1B;
    font-family: 'Spectral', serif;
    font-size: 65px;
  }
  .page-footer{
    background-color: #4C1B1B;
  }
  body {
    display: flex;
    min-height: 100vh;
    flex-direction: column;
  }
  main {
    flex: 1 0 auto;
  }
</style>