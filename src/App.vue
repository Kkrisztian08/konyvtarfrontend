<template>
  <div id="app" class="container">
    <header><h1>Petrik Könyvtár Nyilvántartó</h1></header>
      <nav>
        <ul class="nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#newbook">Új könyv felvétele</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="https://petrik.hu">Petrik honlap</a>
          </li>
        </ul> 
      </nav>
      <main class="row">
        <BookItem class="col-12 col-md-6 col-xl-4" 
        v-for="book in books" 
        v-bind:key="book.id"
        :book="book" />
      </main>
      <BookForm id="newbook" @newbook="Reload"/>
    <footer>Készítette: Kovács Krisztián</footer>
  </div>
</template>

<script>
import BookItem from './components/BookItem.vue'
import BookForm from './components/BookForm.vue'

export default {
  name: 'App',
  components: {
    BookItem,
    BookForm
  },
  data(){
      return{
        books:[]
      }
    },
    methods:{
      async Reload(){
        let Response = await fetch('http://127.0.0.1:8000/api/books')
        let data= await Response.json()
        console.log(data)
        this.books=data.data
      }
    },
    async mounted(){
      this.Reload()
    },
}
</script>

<style>

</style>
