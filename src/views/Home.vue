<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png" />
        <movie-list></movie-list>
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
};
</script>
