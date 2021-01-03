<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png" />
        <saved-movies :movies="savedMovies" @remove-movie="removeMovie" />
        <movie-list @save-movie="saveMovie" />
    </div>
</template>

<script>
// @ is an alias to /src
import MovieList from "../components/MovieList.vue";
import SavedMovies from "../components/SavedMovies.vue";

export default {
    name: "Home",
    components: {
        MovieList,
        SavedMovies,
    },
    data: function () {
        return {
            savedMovies: window.localStorage.getItem("savedMovies")
                ? JSON.parse(window.localStorage.getItem("savedMovies"))
                : [],
        };
    },
    methods: {
        saveMovie: function (movie) {
            if (
                this.savedMovies.find((element) => {
                    return element.id === movie.id;
                })
            ) {
                return;
            }
            this.savedMovies.push(movie);
            this.updateLocalStorage();
        },
        removeMovie: function (movie) {
            const index = this.savedMovies.findIndex((element) => {
                return element.id === movie.id;
            });

            this.savedMovies.splice(index, 1);
            this.updateLocalStorage();
        },
        updateLocalStorage: function () {
            window.localStorage.setItem(
                "savedMovies",
                JSON.stringify(this.savedMovies)
            );
        },
    },
};
</script>
