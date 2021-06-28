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
        {
          username: "iPythonistaBot",
          text: "RT @Strat_AI: 5 Top #Cybersecurity Threats to Businesses \n#100DaysOfCode #AI #Analytics #ArtificialIntelligence #DataScience #DeepLearning…",
          full_name: "Pythonista Bot",
          tweet_url:
            "urhttps://twitter.com/1337430590241562626/status/1409600186133929996",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1337438624296693762/490yTsEo_normal.jpg",
          created_at: "Mon Jun 28 19:50:48 +0000 2021",
          lang: "en",
        },
        {
          username: "fluttbot",
          text: "RT @Strat_AI: 5 Top #Cybersecurity Threats to Businesses \n#100DaysOfCode #AI #Analytics #ArtificialIntelligence #DataScience #DeepLearning…",
          full_name: "Flutter 🤖",
          tweet_url:
            "urhttps://twitter.com/1277715645430468608/status/1409600185936846851",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1279076808529530880/bA7hPPiQ_normal.jpg",
          created_at: "Mon Jun 28 19:50:48 +0000 2021",
          lang: "en",
        },
        {
          username: "Bills_Bot",
          text: "RT @HelpBiology: Hire us to help you with your papers at fair rates\n#Essay \n#Javascript\n#onlineclasses\nPhilosophy \n#Chemistry\n#Literature\n#…",
          full_name: "Bills Bot",
          tweet_url:
            "urhttps://twitter.com/1364497572509880322/status/1409600146292285442",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1409184856685174788/hb_i7LvR_normal.jpg",
          created_at: "Mon Jun 28 19:50:38 +0000 2021",
          lang: "en",
        },
        {
          username: "cybersec_feeds",
          text: "RT @Strat_AI: 5 Top #Cybersecurity Threats to Businesses \n#100DaysOfCode #AI #Analytics #ArtificialIntelligence #DataScience #DeepLearning…",
          full_name: "Cyber Security Feed",
          tweet_url:
            "urhttps://twitter.com/1131854274223366144/status/1409600163887341573",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1131855016766124032/vhasETOF_normal.jpg",
          created_at: "Mon Jun 28 19:50:42 +0000 2021",
          lang: "en",
        },
        {
          username: "jfversluis",
          text: "RT @MiriamAsensi: 5 Ways to Contribute to Open-Source That Doesn’t Involve Writing Code 💥\n#hclswlobp #javascript #github #nodejs #cybersec…",
          full_name: "Gerald Versluis",
          tweet_url:
            "urhttps://twitter.com/31391457/status/1409600146313199621",
          user_profile_image:
            "http://pbs.twimg.com/profile_images/1298992025732182018/_SfrBsMD_normal.jpg",
          created_at: "Mon Jun 28 19:50:38 +0000 2021",
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