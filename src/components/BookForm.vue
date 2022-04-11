<template>
  <form>
    <div v-if="vanHiba" class="alert alert-danger" role="alert">
        {{this.message}}
    </div>
    <div >
        <label for="booktitle" class="form-label">Cím</label>
        <input v-model="book.title" type="text" class="form-control" id="booktitle">
    </div>
    <div >
        <label for="bookauthor" class="form-label">Szerző</label>
        <input v-model="book.author" type="text" class="form-control" id="bookauthor">
    </div>
    <div >
        <label for="bookpublishyear" class="form-label">Kiadás Éve</label>
        <input v-model="book.publish_year" type="number" class="form-control" id="bookpublishyear">
    </div>
    <div >
        <label for="bookpagecount" class="form-label">Oldalszám</label>
        <input v-model="book.page_count" type="number" class="form-control" id="bookpagecount">
    </div>
    <button @click="newBook" class="btn btn-primary">Új könyv</button>
  </form>
</template>

<script>
export default {
    name: 'BookForm',
    data(){
        return{
            vanHiba:false,
            message:'',
            book:{
                title: '',
                author: '',
                publish_year: '',
                page_count: '',
            }
        }
    },
    methods:{
        async newBook(){
            let Response =await fetch('http://127.0.0.1:8000/api/books', {
                method: "POST",
                headers:{
                    'Content-Type':'application/json',
                    'Accept':'application/json' 
                },
                body: JSON.stringify(this.book)
            })
            let body=await Response.json()
            if (Response.status ==201){
                this.vanHiba=false
                this.book= {
                    title: '',
                    author: '',
                    publish_year: '',
                    page_count: '',
                }
                this.$emit("newbook")
                return
            }
            this.vanHiba=true
            this.message= body.message
            //alert('New Book');
            }   
        }
    }
</script>

<style>

</style>