  <template>
  <ul
    role="list"
    class="
      grid grid-cols-1
      gap-0
      sm:grid-cols-2
      sm:gap-x-6
      lg:grid-cols-3
      xl:gap-x-8
    "
  >
    <li
      v-for="(tweet, index) in tweets.filter((tweet) => tweet.lang === 'en')"
      :key="index"
      class="relative"
    >
      <div class="w-full h-full">
        <Tweet :tweet="tweet" />
      </div>
    </li>
  </ul>
</template>

<script>
import Tweet from "./Tweet.vue";

import Pusher from "pusher-js";

const PUSHER = new Pusher(process.env.NUXT_ENV_PUSHER_APP_KEY, {
  cluster: process.env.NUXT_ENV_PUSHER_CLUSTER,
});

const CHANNEL = "tweets";

const EVENT = "new-tweet";

export default {
  components: {
    Tweet,
  },
  data() {
    return {
      tweets: [
        {
          username: "1000dayscodingb",
          text: "RT @Paula_Piccard: Google considered using drones for firefighting\nhttps://t.co/t0E6mTa2Wf @CNET \n#MachineLearning #5G #DataScience #100D…",
          full_name: "1000 Days Of Coding - BOT",
          tweet_url:
            "https://twitter.com/1347291458278080513/status/1409170257630035975",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1377718369844011009/5JZNdqVy_normal.jpg",
          created_at: "Sun Jun 27 15:22:25 +0000 2021",
          lang: "en",
        },
      ],
    };
  },

  mounted() {
    const channel = PUSHER.subscribe(CHANNEL);
    channel.bind(EVENT, (data) => {
      this.tweets.push(data);
    });
  },

  beforeDestroy() {
    PUSHER.unsubscribe(CHANNEL);
  },
};
</script>