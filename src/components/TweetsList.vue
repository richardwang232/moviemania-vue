<template>
    <div class="tweets-container">
        <h2 v-if="movie">
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
export default {
    name: "TweetsList",
    props: {
        movie: Object,
        tweets: Array,
    },
};
</script>

<style lang="scss" scoped>
.tweets-container {
    width: 500px;
    border: 3px solid blue;
    border-radius: 5px;
    margin: auto;
}

// .tweets {
//     display: inline-block;
//     position: absolute;
//     right: 0;
//     top: 0;
//     bottom: 0;
//     left: 50%;
//     overflow-y: scroll;
//     border: 1px solid #cccccc;
// }

li {
    list-style-type: none;
}
</style>