<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col">

                <h3> ¿Seguro desea eliminar el libro?</h3>

                <p>titulo: {{ this.element.title }}</p>
                <p>Descripcion {{ this.element.description }}</p>

            </div>
        </div>
        <div class="row">
            <div class="col">

            <b-button v-on:click="deleteBook" variant="danger">Eliminar</b-button>

            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert'

export default {
    data (){
        return {
            bookId: this.$route.params.bookId,
            element: {
                title: '',
                description: '',
            }
        }
    },

    methods: {
        getBook(){
            const path = `${process.env.BASE_URI}books/${this.bookId}/`

            axios.get(path).then((response) => {
                this.element.title = response.data.title
                this.element.description = response.data.description
            })
            .catch((error) => {
                console.log(error)
            })
        },
        deleteBook(){
            const path = `${process.env.BASE_URI}books/${this.bookId}/`

            axios.delete(path).then((response) => {
                location.href= '/Books'
            })
            .catch((error) => {
                swal("No es posible eliminar el libro", "", "error")
            })
        }
            
    },
    created(){
        this.getBook()
    }
}
</script>

<style lang="css" scoped>
</style>