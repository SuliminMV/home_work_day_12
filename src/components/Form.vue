<template>
    <div class="form">
        <fieldset>
            <legend>Добавьте новую книгу в библиотеку</legend>
            <label>Книга</label>
            <input v-model:value="title" placeholder="Название" type="text">
            <br>
            <label>Автор</label>
            <input v-model:value="author" placeholder="Фамилия Имя" type="text">
            <br>
            <label>Выпуск</label>
            <input v-model:value="publication" placeholder="Год публикации" type="number">
            <br>
            <label>Жанр</label>
            <select v-model:value="genre">
                <option value="Фантастика">Фантастика</option>
                <option value="Роман">Роман</option>
                <option value="Детектив">Детектив</option>
            </select>
            <br>
            <button v-if="item === null" v-on:click="addNewBook">Добавить книгу</button>
            <div v-else>
                <button v-on:click="saveButtonClicked">Сохранить</button>
                <button v-on:click="$emit('back')">Назад</button>
            </div>
        </fieldset>
        <h1 align="center">Список книг:</h1>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                title: null,
                author: null,
                publication: null,
                genre: null,
            }
        },
        props: ['item'],
        watch: {
            item: function (val) {
                if (this.item !== null) {
                    this.title = val.title;
                    this.author = val.author;
                    this.publication = val.publication;
                    this.genre = val.genre;
                } else {
                    this.title = null;
                    this.author = null;
                    this.publication = null;
                    this.genre = null;
                }
            }
        },
        methods: {
            addNewBook: function () {
                this.$emit('addBook', {
                    title: this.title,
                    author: this.author,
                    publication: this.publication,
                    genre: this.genre
                });
                this.title = null;
                this.author = null;
                this.publication = null;
            },
            saveButtonClicked: function () {
                this.$emit('updateBook', {
                    number: this.item.number,
                    title: this.title,
                    author: this.author,
                    publication: this.publication,
                    status: this.item.status
                });

            },
        }


    }
</script>

<style>
    fieldset {
        border-radius: 30px;
        text-align: center;
    }

    input, select {
        margin: 5px 0;
    }


    legend {
        font-size: 25px;
        text-align: center;
        font-weight: bold;
    }

    button {
        background-color: #107f1d;
        border: 2px solid silver;
        border-radius: 10px;
        color: wheat;
        margin: 5px;
    }

</style>