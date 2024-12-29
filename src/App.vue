<template>
   <div class="container">
      <div class="verse-card">
          <!-- <h1>12/28 Wednesday</h1>
          <p>{{ verseData }}</p>
          <small>Genesis 15:1</small> -->
          <template v-for="verse in bibleVerses" :key="verse" >
            <span style="display:block; text-align: left;">{{ verse.reference }} – {{ verse.text }}</span>
          </template>
      </div>

  </div>
</template>

<script>
import { bibleVerses } from './const/verse';
// import bibleVerses from './const/verse.js'
export default {
  name: 'App',
  components: {
  },
  data() {
      return {
        bibleVerses
      };
  },
  mounted(){
    console.log(this.bibleVerses)
  }
}
</script>

<style>
body {
    margin: 0;
    padding: 0;
    background: url('../public/img/bg.jpg') no-repeat center center fixed;
    background-size: cover;
    color: white;
    font-family: Arial, sans-serif;
    height: 100vh;
}
.container {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.verse-card {
  /* width: 90vw;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translate(-50%,-50%);

  background-color: rgba(0, 0, 0, 0.7);
  padding: 20px;
  border-radius: 10px;
  text-align: center; */
}
.verse-card h1 {
    font-size: 1.5rem;
}
.verse-card p {
    font-size: 1.2rem;
    text-align: left;
}
small {
  display: block;
    /* position: absolute; */
    bottom: 10px;
    width: 100%;
    text-align: right;
}
</style>
