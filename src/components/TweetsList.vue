<template>
    <div class="tweets-container">
        <h2>
            <i class="fa fa-twitter"></i>Relevant Tweets for
            <em>{{ movie.title }}</em>
        </h2>

        <img
            class="ajax-loader"
            src="/public/ajax-loader.gif"
            style="display: none"
        />

        <div class="tweets">
            <ul v-if="tweets && tweets.length">
                <li v-for="tweet in tweets" :key="tweet.id">
                    <div>
                        <img :src="tweet.user.profile_image_url" /><em>{{
                            tweet.user.screen_name
                        }}</em>
                        <p style="float: right">
                            <em>{{ tweet.created_at }}</em>
                        </p>
                    </div>
                    <p>{{ tweet.text }}</p>
                </li>
            </ul>
            <div v-if="!tweets || !tweets.length">No tweets</div>
        </div>
    </div>
</template>

<script>
// import Codebird from "../../codebird.js";
export default {
    name: "TweetsList",
    props: {
        movie: Object,
        tweets: Array,
    },
    data: function () {
        return {
            cb: null,
        };
    },
    computed: function () {
        return {};
    },
    created() {
        //this only needs to be done once, get bearer token for OAuth Twitter
        // this.cb = new Codebird();
        // this.cb.setConsumerKey(
        //     "dJubmPzGfaSiM4z6enh5Pw",
        //     "QdulpG2gTkfftg2yaGxYYgbqTwF3BoARsqizRi54rc"
        // );
        // this.cb.__call("oauth2_token", {}, function (reply) {
        //     var bearer_token = reply.access_token;
        // });
    },
    methods: {
        getTweets: function (movie) {
            // this.cb.__call(
            //     "search_tweets",
            //     "q=" + encodeURIComponent(movie.title) + "&lang=en",
            //     function (response) {
            //         debugger;
            //         //some jquery promise action
            //         //that.reset(that.parse(response));
            //         //that.promise.resolve();
            //     },
            //     true // this parameter required
            // );
        },
        parse: function (response) {
            return response.statuses;
        },
    },
};
</script>

<style lang="scss" scoped>
li {
    list-style-type: none;
}
</style>