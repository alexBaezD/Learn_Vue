<template>
  <div class="comments">
    <img
      src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/vue-post-photo.jpg"
      class="main-photo"
    />
    <img
      src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/vue-main-profile.jpg"
      class="main-profile"
    />
    <div class="main-info">
      <span class="name">Julianne Delfina</span>
      <h3>"It's lovely after it rains"</h3>
    </div>
    <hr />
    <ul>
      <individual-comment
        v-for="(comment, i) in comments"
        :key="i"
        v-bind:commentpost="comment"
      ></individual-comment>
    </ul>
    <input
      v-model="newComment"
      v-on:keyup.enter="addComment"
      placeholder="Add a comment press enter"
      type="text"
    />
    <br />
    <p>Last comment {{ lastComment }}</p>
  </div>
</template>

<script>
import IndividualComment from "../components/IndividualComment";
export default {
  components: {
    IndividualComment
  },
  data() {
    return {
      newComment: " "
    };
  },
  computed: {
    comments() {
      return this.$store.state.comments;
    },
    lastComment() {
      return this.$store.getters.lastComment;
    }
  },
  methods: {
    addComment() {
      this.$store.commit("addComment", this.newComment);
      this.newComment = "";
    }
  }
};
</script>

<style scoped>
.comments {
  background: #212222;
  color: #fff;
  letter-spacing: 0.04em;
  text-align: center;
  width: 370px;
  margin: 2em auto;
  display: table;
  padding: 20px;
  line-height: 1.4em;
}
.name {
  color: #ccc;
}
small {
  color: #bbb;
  font-size: 10px;
}
h3 {
  margin: 5px 0 4px;
}
.main-photo {
  width: 300px;
}
.main-profile {
  float: left;
  border: 3px solid white;
  margin: -25px 0 0 20px;
  position: relative;
  width: 80px;
}
.main-info {
  float: left;
  padding: 10px 20px;
  text-align: left;
  margin-bottom: 15px;
}
.main-info::after {
  content: "";
  display: table;
  clear: both;
}
li {
  list-style: none outside none;
  text-align: left;
  padding: 10px 0;
  border-bottom: 1px solid #555;
}
ul {
  margin: 0;
  padding: 0 35px;
}
hr {
  margin: 25px 0 0 32px;
  width: 300px;
  border-top: 0;
  border-bottom: 1px solid #555;
}
input {
  font-family: "Playfair Display", serif;
  width: 280px;
  margin: 30px 0;
  padding: 8px 10px;
  outline: 0;
}
</style>
