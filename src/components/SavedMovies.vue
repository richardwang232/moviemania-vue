<template>
    <ul class="saved-movies">
        <li
            v-for="movie in movies"
            :key="movie.id"
            :data-id="movie.id"
            :data-title="movie.title"
            class="item saved-movies__item"
        >
            {{ movie.title }}
            <a @click="removeMovie" href="#" class="delete-movie"
                ><i class="fa fa-minus"></i
            ></a>
            <a @click="getTweets" href="#" class="show-tweets"
                ><i class="fa fa-twitter"></i
            ></a>
        </li>
    </ul>
</template>

<script>
export default {
    name: "SavedMovies",
    props: {
        movies: Array,
    },
    methods: {
        removeMovie: function (e) {
            const item = e.target.closest(".item");
            const title = item.dataset.title;
            const id = item.dataset.id;
            this.$emit("remove-movie", {
                title: title,
                id: id,
            });
        },
        getTweets: function (e) {
            const item = e.target.closest(".item");
            const title = item.dataset.title;
            const id = item.dataset.id;
            this.$emit("get-tweets", {
                title: title,
                id: id,
            });
        },
    },
};
</script>

<style lang="scss">
.saved-movies {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}
.saved-movies__item {
    font-size: 1.75rem;
}
</style>