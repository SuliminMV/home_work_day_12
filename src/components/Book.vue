<template>
            <div v-bind:class="`book ${item.status}`">
            <h2>Книга &#8470 {{item.number}} - {{bookStatus}}  </h2>
            <h3>Название: "{{item.title}}"</h3>
            <h4>Автор: {{item.author}}</h4>
            <h4>Год публикации: {{item.publication}}</h4>
            <h4>Жанр: {{item.genre}} </h4>
            <div class="controls">
                <button v-if="item.status != 'read'" v-on:click="readBook">Прочитано</button>
                <button v-on:click="editBook">Редактировать</button>
                <button v-on:click="deleteBook">Удалить</button>
            </div>
        </div>
    </template>

<script>
    export default {
        name:'Book',
        props:['item'],
        computed: {
            bookStatus: function () {
                switch(this.item.status) {
                    case 'unread':
                        return 'Не прочитана';
                    case 'read':
                        return 'Прочитана'
                }
            }
        },
        methods:{
            deleteBook:function() {
                this.$emit('deleteBook',this.item.number);
            },
            editBook:function() {
                this.$emit('editBook',this.item.number);
            },
            readBook:function () {
                this.$emit('readBook',this.item.number);
            }

        }

    }
</script>

<style>
    h2 {
        font-style: italic;
    }

    .book {
        border: 1px solid black;
        border-radius: 30px;
        text-align: center;
        padding: 5px;
        margin: 10px;
    }
    .book.read {
        background-color: #107f1d;
    }
    button {
        background-color: #107f1d;
        border: 2px solid silver;
        border-radius: 10px;
        color: wheat;
    }
</style>