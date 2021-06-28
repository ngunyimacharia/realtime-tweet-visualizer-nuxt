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
      tweets: [],
      defaultTweets: [
        {
          username: "Pariveda_Inc",
          text: "How do you find your best customers when you're lacking #data and a centralized industry? Find out how out-of-the-box thinking can lead to meaningful insights with our free on-demand video content. https://t.co/hEjRjK5PLQ\n#Data #MDE #ModernData https://t.co/SRcuMvj8x7",
          full_name: "Pariveda Solutions",
          tweet_url:
            "urhttps://twitter.com/314632270/status/1409598034950995971",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/869672766726746112/HcOfk8nf_normal.jpg",
          created_at: "Mon Jun 28 19:42:15 +0000 2021",
          lang: "en",
        },
        {
          username: "CodingNinjaBOT",
          text: "RT @Dailycodinghab1: Java Code quiz \nWhat is the Output? \n#java #javaprogramming #datascience  #webdeveloper #web  #programming #codingcha…",
          full_name: "Coding NinjaBOT 🤖",
          tweet_url:
            "urhttps://twitter.com/1229842670710902785/status/1409600199614468097",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1229848030960115712/W3TebBgV_normal.jpg",
          created_at: "Mon Jun 28 19:50:51 +0000 2021",
          lang: "en",
        },
        {
          username: "hubofml",
          text: "RT @MiriamAsensi: 5 Ways to Contribute to Open-Source That Doesn’t Involve Writing Code 💥\n#hclswlobp #javascript #github #nodejs #cybersec…",
          full_name: "HubOfML",
          tweet_url:
            "urhttps://twitter.com/3040871649/status/1409600169906216962",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1254334743333818373/F3xeh1db_normal.jpg",
          created_at: "Mon Jun 28 19:50:44 +0000 2021",
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

    this.addDefaultTweets();
  },

  methods: {
    addDefaultTweets() {
      setTimeout(() => this.tweets.push(this.defaultTweets[0]), 1000);
      setTimeout(() => this.tweets.push(this.defaultTweets[1]), 2000);
      setTimeout(() => this.tweets.push(this.defaultTweets[2]), 3000);
    },
  },
  beforeDestroy() {
    PUSHER.unsubscribe(CHANNEL);
  },
};
</script>