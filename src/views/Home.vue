<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png" />
        <movie-list :movies="movies"></movie-list>
    </div>
</template>

<script>
// @ is an alias to /src
import MovieList from "../components/MovieList.vue";

export default {
    name: "Home",
    components: {
        MovieList,
    },
    data: function () {
        return {
            movies: ["foo", "bar", "baz"],
        };
    },
};
</script>
