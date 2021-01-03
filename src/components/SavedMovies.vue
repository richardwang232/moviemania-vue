<template>
    <ul>
        <li
            v-for="movie in movies"
            :key="movie.id"
            :data-id="movie.id"
            :data-title="movie.title"
            class="item"
        >
            {{ movie.title }}
            <button class="remove-btn" @click="removeMovie">Remove</button>
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
    },
};
</script>

<style lang="scss">
</style>