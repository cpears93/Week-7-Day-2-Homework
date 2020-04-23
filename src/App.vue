<template lang="html">
  <div id="app">
    <header>
      <h1 class="title">Twitter</h1>
    </header>
    <section class="tweet-forms">
      <h3 id="total-likes">Total Likes: {{totalLikes}}</h3>
      <form v-on:submit.prevent="saveTweet">
        <h3>Add Tweet</h3>
        <input placeholder="Name" type="text" v-model="newTweet.name" />
        <input placeholder="Handle" type="text" v-model="newTweet.handle" />
        <textarea placeholder="Your tweet..." rows="2" cols="50" maxlength="280" v-model="newTweet.tweet"/>
        <input type="submit" value="Add Tweet"/>
      </form>
      <div id="filterTweet">
        <h3>Filter Tweets By Minimum likes</h3>
        <input  type="number" v-model.number="likeAmount"/>
      </div>
    </section>
    <section class="tweet-list">
      <tweet-list-item v-for="(tweet, index) in filteredTweets" :key="index" :tweet="tweet"></tweet-list-item>
    </section>
  </div>
</template>

<script>
import TweetListItem from './components/TweetListItem.vue';

export default {
  name: 'app',
  components: {
    'tweet-list-item': TweetListItem
  },
  data() {
    return {
      tweets:[
        {
          id: 1,
          name: 'James',
          handle: '@jokerjames',
          img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
          tweet: "If you don't succeed, dust yourself off and try again.",
          likes: 10,
        },
        {
          id: 2,
          name: 'Fatima',
          handle: '@fantasticfatima',
          img: 'https://semantic-ui.com/images/avatar2/large/molly.png',
          tweet: 'Better late than never but never late is better.',
          likes: 12,
        },
        {
          id: 3,
          name: 'Xin',
          handle: '@xeroxin',
          img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
          tweet: 'Beauty in the struggle, ugliness in the success.',
          likes: 18,
        }
      ],
      newTweet: {
        name: '',
        handle: '',
        img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
        tweet: '',
        likes: 20,
      },
      likeAmount: 0
    }
  },
  computed: {
    totalLikes: function(){
      return this.tweets.reduce((total, tweet) => {
        return total + tweet.likes
      }, 0)
    },
    filteredTweets: function(){
      return this.tweets.filter((tweet) => {
        return tweet.likes >= this.likeAmount
      })
    }
  },
  methods: {
    saveTweet: function(){
      this.tweets.unshift(this.newTweet);
      this.newTweet = {
        name: '',
        handle: '',
        img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
        tweet: '',
        likes: 20,
      }
    }
  }
}
</script>

<style lang="css" scoped>
body {
  margin:0px;
}

header {
  background:#F0F0F0;
  border:1px solid #CCC;
  margin:0px auto;
}

.title{
  text-align: center;
  font-family: cursive;
  font-size: 3em;
}

.tweet-list {
  display: flex;
}

form, #filterTweet, #total-likes {
  background: #eee;
  padding: 10px 20px 20px 20px;
  margin-top: 40px;
}

#filterTweet {
  height: 60px;
}

#total-likes {
  height: 20px;
  padding-top: 10px;
  text-align: center;
}

input {
  width: 100%;
}

form textarea {
  width: 100%;
  height: 50px;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  resize: none;
}

.tweet-forms {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  margin:10px;
}
</style>
