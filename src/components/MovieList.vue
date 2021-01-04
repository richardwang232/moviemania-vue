<template>
    <ul class="container">
        <li
            class="item"
            v-for="movie in movies"
            :key="movie.id"
            :data-id="movie.id"
            :data-title="movie.title"
        >
            <div class="poster">
                <img
                    :src="baseUrl + posterSize + movie.poster_path"
                    class="img-responsive"
                />
                <div class="save" @click="saveMovie">
                    <i class="fa fa-plus save-movie"></i>
                </div>
            </div>
            <div class="">
                <h4>{{ movie.title }}</h4>
                Release Date: {{ movie.release_date }} <br />
                Score: <b>{{ movie.vote_average }}</b> <br />
                <button
                    type="button"
                    @click="saveMovie"
                    class="save-movie btn btn-secondary"
                >
                    Add to Favorites
                </button>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    name: "MovieList",
    props: {},
    data: function () {
        return {
            movies: [],
            baseUrl: "",
            posterSize: "",
        };
    },
    created() {
        fetch(
            "https://api.themoviedb.org/3/configuration?api_key=00b1a245c429c285c83f95fbb86180be"
        )
            .then((response) => response.json())
            .then((data) => {
                this.baseUrl = data.images.base_url;
                this.posterSize = data.images.poster_sizes[5];
                return fetch(
                    "https://api.themoviedb.org/3/movie/now_playing?api_key=00b1a245c429c285c83f95fbb86180be"
                );
            })
            .then((response) => response.json())
            .then((data) => {
                this.movies = data.results;
            });
    },
    methods: {
        saveMovie: function (e) {
            e.preventDefault();
            const item = e.target.closest(".item");
            const title = item.dataset.title;
            const id = item.dataset.id;

            this.$emit("save-movie", {
                id: id,
                title: title,
            });
        },
    },
};
</script>

<style lang="scss">
img.resize {
    width: 200px;
    height: auto;
}
ul img {
    border: 3px solid black;
}
.poster:hover .save {
    opacity: 0.4;
}
.poster {
    position: relative;
    display: inline-block;
    cursor: pointer;

    img {
        padding: 1px;
        width: 150px;
        height: 200px;
    }
    .save {
        background-color: #000;
        opacity: 0;
        z-index: 2;
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        text-align: center;
        color: #fff;
        font-size: 4em;
    }
    .save:before {
        content: "";
        display: inline-block;
        height: 100%;
        vertical-align: middle;
        /* margin-right: -0.25em; */
    }
}
.poster.selected img {
    border: 3px solid blue;
}
.container .item {
    display: inline-block;
    margin: 5px;
}
</style>