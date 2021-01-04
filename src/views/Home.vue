<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png" />
        <saved-movies
            :movies="savedMovies"
            @remove-movie="removeMovie"
            @get-tweets="getTweets"
        />
        <tweets-list :movie="tweetedMovie" :tweets="tweets" />
        <movie-list @save-movie="saveMovie" />
    </div>
</template>

<script>
// @ is an alias to /src
import MovieList from "../components/MovieList.vue";
import SavedMovies from "../components/SavedMovies.vue";
import TweetsList from "../components/TweetsList.vue";

export default {
    name: "Home",
    components: {
        MovieList,
        SavedMovies,
        TweetsList,
    },
    data: function () {
        return {
            savedMovies: window.localStorage.getItem("savedMovies")
                ? JSON.parse(window.localStorage.getItem("savedMovies"))
                : [],
            tweetedMovie: null,
            tweets: [],
            cb: null,
            bearer_token: null,
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
        getTweets: function (movie) {
            this.tweetedMovie = movie; // if we want to move logic to TweetsList component
            this.cb.__call(
                "search_tweets",
                "q=" + encodeURIComponent(movie.title) + "&lang=en",
                (response) => {
                    this.tweets = response.statuses;
                },
                true // this parameter required
            );
        },
        updateLocalStorage: function () {
            window.localStorage.setItem(
                "savedMovies",
                JSON.stringify(this.savedMovies)
            );
        },
    },
    created() {
        // this only needs to be done once, get bearer token for OAuth Twitter
        this.cb = new Codebird();
        this.cb.setConsumerKey(
            "dJubmPzGfaSiM4z6enh5Pw",
            "QdulpG2gTkfftg2yaGxYYgbqTwF3BoARsqizRi54rc"
        );
        this.cb.__call("oauth2_token", {}, (reply) => {
            this.bearer_token = reply.access_token;
        });
    },
};
</script>
