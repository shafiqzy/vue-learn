<template>
  <h1>{{ title }}</h1>
  <br>
  <p>Welcome...</p>
  <div v-if="showModal">
    <Modal :header="header" :text="text" theme="sale" @close="toggleModal"/>
  </div>
  <button @click.alt="toggleModal">Open Modal (alt)</button><!--.alt is modifier-->
</template>

<script>
  import Modal from './components/Modal.vue'

  export default{
    name:'app',
    components: {Modal},
      data(){
        return{
          title:'The Waterfall Vue App Modal Test',
          header: 'Sign up for the Giveaway!',
          text: 'Grab your ninja swag for half price!',
          showModal: false
        }
      },
      methods:{
        toggleModal(){
          this.showModal = !this.showModal
        }
      }
  }
</script>

<style>
#app{
  font-family: Avenir, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:#2c3e50;
  margin-top: 60px;
}

h1{
  border-bottom:1px solid #ddd;
  display:inline-block;
  padding-bottom: 10px;
}
</style>