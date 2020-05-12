<template>
    <div id="app">
        <Form v-bind:item="editingBook" v-on:back="editingBook = null" v-on:addBook="addNewBookListener" v-on:updateBook="updateBookListener"/>
        <Book v-for="book in library" v-bind:item="book" v-on:readBook="readBookListener"
              v-on:editBook="editBookListener" v-on:deleteBook="deleteBookListener"/>
    </div>
</template>

<script>
    import form from './components/Form.vue'
    import book from './components/Book.vue'

    export default {
        data: function () {
            return {
              editingBook: null,
                library: [
                    {
                        number: 1,
                        title: 'Гарри Поттер и философский камень',
                        author: 'Роулинг Джоан',
                        publication: 1997,
                        genre: 'Фантастика',
                        status: 'read'
                    },
                    {
                        number: 2,
                        title: 'Муравьи',
                        author: 'Вербер Бернар',
                        publication: 2005,
                        genre: 'Роман',
                        status: 'unread'
                    },
                    {
                        number: 3,
                        title: 'Война и мир',
                        author: 'Толстой Лев',
                        publication: 1865,
                        genre: 'Роман',
                        status: 'unread'
                    },
                    {
                        number: 4,
                        title: 'Собака Баскервилей',
                        author: 'Конан Дойл Артур',
                        publication: 1901,
                        genre: 'Детектив',
                        status: 'unread'
                    }
                ]
            }
        },
        name: 'App',
        components: {
            Form: form,
            Book: book
        },
        methods: {
            readBookListener: function (number) {
                let finishedBook = this.library.find((el) => el.number === number);
                if (finishedBook) {
                    finishedBook.status = 'read';
                }
            },
            fetchMaxId: function () {
                return Math.max.apply(Math, this.library.map((o) => o.number));
            },
            addNewBookListener: function (item) {
                item.number = this.fetchMaxId() + 1;
                item.status = 'unread';
                this.library.push(item);
            },
            deleteBookListener:function(number) {
                let bookIndex = this.library.findIndex((el) => el.number === number);
                if (bookIndex >= 0) {
                    this.library.splice(bookIndex, 1);
                }
            },
            updateBookListener: function(item) {
                let bookIndex = this.library.findIndex((el) => el.number === item.number);
                if (bookIndex >= 0) {
                    this.library.splice(bookIndex, 1, item);
                    this.editingBook = null;
                }
            },
            editBookListener: function(number) {
              let bookIndex = this.library.findIndex((el) => el.number === number);
              if (bookIndex >= 0) {
                this.editingBook = this.library[bookIndex];
                  console.log(this.library[bookIndex])
              }
            }
        }
    }
</script>

<style>

    #app {
    }
</style>
