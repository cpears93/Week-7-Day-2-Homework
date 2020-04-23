<template lang="html">
  <div class="tweet-list-item">
    <div class="avatarContainer">
      <img :src="tweet.img" class="avatar" width="70" height="70">
    </div>
    <div class="tweetBody">
        <h4 class="author">
          {{ tweet.handle }}
        </h4>
      <div class="tweetContent">
        <p> {{ tweet.tweet }}</p>
        &#128077; {{ tweet.likes }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'tweet-list-item',
  props: ['tweet']
}
</script>

<style lang="css" scoped>

.tweet-list-item {
  height: 250px;
  width: 50vw;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 10px;
  border: solid 1px black;
  margin:5px;
}

.tweetBody {
  padding:10px;
  text-align: center;
  background-color: rgba(175,238,238, 0.5);

}

.avatarContainer {
  margin-right: 20px;
  text-align: center;
}
.avatar {
  margin-top: 3px;
  border-radius: 50%;
}
</style>
