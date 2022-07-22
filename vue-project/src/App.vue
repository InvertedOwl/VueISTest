<script>
  const API = "https://is.invertedowl.com/api/boards"

  export default {
    data: () => {
      return {
        boards: {},
        limit: 2,
        imgs: "https://brohouse.dev/usr/image/"
      }
    },
    
    methods: {
      async fetchBoards() {
        this.boards = null
        this.boards = await (await fetch(API, {method: "GET", headers: {"order": "new", "limit": this.limit, "offset": "0", }})).json()
      }
    }
  }

</script>

<template>
  <h1>VUE idiotscript boards!</h1>
  <label for="limit-input">Limit</label>
  <form @submit.prevent="fetchBoards">
    <input type="number" v-model="limit" class="limit" id="limit-input">
    <button type="submit">Submit</button>
  </form>

  <ul v-if="boards" class="ul">
    <li v-for="board in Object.keys(boards)" class="li">
      <p class="p"><span><img :src="imgs + boards[board].username + '.png'" class="img"></span> {{boards[board].name}} - <span class="board">{{board}}</span></p>
    </li>
  </ul>
  <h1 v-else>
    Loading...
  </h1>

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Merienda&display=swap');

body {
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 700;
  background-color: rgb(159, 159, 159);
}

.limit {
  width: 50px;
}

.board {
  font-weight: 100;
  font-style: italic;
  display: inline-block;
}

.img {
  aspect-ratio: 1/1;
  display: inline-block;
  width: 50px;
}
.ul {
  list-style: none;
  padding: 0px !important;
  margin: 0px;
    line-height: 50px;

}


</style>
