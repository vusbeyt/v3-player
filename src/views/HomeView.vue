<template>
<div class="music-player">
  <div class="player-container">
  <section>
    <h2 class="song-title">{{ current.title }}</h2>
    <div class="controls">
<img src="../assets/prev.png" class="prev button" @click="prev">
<img src="../assets/play.png" class="play button" v-if="!isplaying" @click="play">
<img src="../assets/pause.png" class="pause button" v-else @click="pause">
<img src="../assets/next.png"  class="next button" @click="next">
    </div>
  </section>
  </div>
</div>
</template>
<style>
.song-title{
  font-weight: 700;
  font-size: 24px;
  margin-bottom: 10px;
}
.player-container{
max-width: 700px;
margin: 0 auto;
text-align: center;
}
.music-player{
  width: 100%;
  height: 7vh;
  position: absolute;
  background: rgb(0 0 0 / 10%);
  bottom: 0;
}
.controls{
  display: flex;
  justify-content: center;
}
.button{
  width: 20px;
  height: 20px;
  cursor: pointer;
  margin: 0 20px;
}
</style>
<script>
export default {
  data: () => {
    return {
      current: {},
      index: 0,
      isplaying: false,
      songs: [
        {
          title: 'Morgenshtern',
          src: '../src/assets/bass1.mp3'
        },
        {
          title: 'bass music 2',
          src: '../src/assets/bass2.mp3'
        },
        {
          title: 'bass music 3',
          src: '../src/assets/bass3.mp3'
        }
      ],
      player: new Audio()
    }
  },
  methods: {
  play (song) {
    if (typeof song.src != "undefined") {
      this.current = song;

      this.player.src = this.current.src;
    }

    this.player.play();
    this.isplaying = true;
  },
  pause () {
    this.player.pause();
    this.isplaying = false;
  },
  next () {
this.index++
if (this.index > this.songs.length - 1) {
  this.index = 0;
}

this.current = this.songs[this.index];
this.play(this.current);
  },
  prev () {
    this.index--
if (this.index < 0) {
  this.index = this.songs.length - 1;
}

this.current = this.songs[this.index];
this.play(this.current);
  }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>