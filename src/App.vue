<template>
  <div class="music-player">
    <h1>lets play music</h1>
    <div class="title">
      <h5>{{songs[currentIndex].title}}</h5>
    </div>
    <div class="buttons">
    <div class="prev">
      <button @click="prev"><i class="fa fa-step-backward"/></button>
    </div>
      <div v-show="!isPlaying" class="play">
      <button @click="playMusic"><i class="fa fa-play"/></button>
    </div>
    <div class="pause">
      <button v-show="isPlaying" @click="pause"><i class="fa fa-pause"/></button>
    </div>
    <div class="next">
      <button @click="next"><i class="fa fa-step-forward"/></button>
    </div>
    </div>
    <div class="music-list">
      <h5>Music List</h5>
      <div class="music-title" v-for="(song, index) in songs" :key="song.id">
        <button :class="(current.song === song.song) ? 'active' : null " @click='play(song, index)'>{{song.title}}</button>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data (){
    return {
      songs:[
        {id:1, title: 'Dont-say-No', song: require('@/assets/music/dont-say-no.mp3')},
        {id:2, title: 'Scatter', song: require('@/assets/music/scatter.mp3')},
        {id:3, title: 'Voice', song: require('@/assets/music/voice.mp3')},
        {id:4, title: 'Do-like-I-Do', song: require('@/assets/music/do-like-i-do.mp3')},
        {id:5, title: 'Need-You', song: require('@/assets/music/Need-you.mp3')},
      ],
      player: new Audio(),
      currentIndex:0,
      isPlaying:false,
      current:'',
    }
  },
  created(){
    this.player.src = this.songs[this.currentIndex].song;
    this.current = this.songs[this.currentIndex]
    this.player.play()
    this.isPlaying = true
    
  },
  methods:{
    play(song){
      if(typeof song !== undefined){
        this.current = song
          this.player.src = this.current.song;
         
      }
       this.currentIndex = song.id - 1 ;
        this.player.play()
        this.isPlaying = true;
        
        this.player.addEventListener('ended', function(){
          this.currentIndex++
          console.log(this.currentIndex)
          if(this.currentIndex > this.songs.length - 1){
            this.currentIndex = 0;
          }
          this.current = this.songs[this.currentIndex];
          this.play(this.current)
        }.bind(this))
    },
    playMusic(){
      this.player.play()
      this.isPlaying = true;
    },
    pause(){
        this.player.pause()
        this.isPlaying = false;
    },
    next(){
      this.currentIndex++;
      if(this.currentIndex > this.songs.length - 1){
            this.currentIndex = 0;
          }
      this.current = this.songs[this.currentIndex];
      this.player.src = this.current.song
      this.player.play()
       
    },
    prev(){
      this.currentIndex--;
      if(this.currentIndex < 0){
        this.currentIndex = this.songs.length - 1
      }
      this.current = this.songs[this.currentIndex];
      this.player.src = this.current.song
      this.player.play()
    }
  }
}
</script>

<style>
.music-player{
  width: 500px;
  background: linear-gradient(25deg, #006cb6, #e6007e);
 margin: 10px auto;
 overflow: hidden;
}
.music-player h1{
  width: 100%;
  text-align: center;
  color: #fff;
  font-family: Monotype Corsiva, sans-serif ;
  margin: auto;
  margin-bottom: 5px;
  margin-top: 10px;
}
.music-list{
  display: flex;
  flex-direction: column;
  width: initial;
  justify-content: center;
  align-items: center;
}
.music-list .music-title{
  width:500px;
  margin: 10px;
}
.music-list .music-title button:hover{
  transform: translateX(-10px);
  opacity: 0.7;
}
.music-list .music-title button{
  appearance: none;
  border: none;
  outline: none;
  margin-top: -5px;
  padding: 15px 15px;
  width: 100%;
  color: white;
  font-weight: 800;
  cursor: pointer;
  transition: all .2s linear;
  background: #e6007e;
}
.music-list .music-title button.active{
  background: black;
}
.music-list h5{
  width: 500px;
  text-align: center;
  font-size: 25px;
  padding: 5px 15px;
  color: #fff;
}
.title{
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 500px;
  font-size: 22px;
  color: #fff;
}
.buttons{
  display: flex;
  max-width: 500px;
  justify-content: center;
  align-items: center;
  margin: 10px auto;
}
.buttons button i{
  font-size: 25px;
}
.buttons button{
  appearance: none;
  border: none;
  outline: none;
  padding: 10px 25px;
  background: #6743f8;
  color: #fff;
  border-radius: 5px;
  font-weight: 600;
  cursor: pointer;
  transition:.2s linear;
  margin-left: 10px;
}
.buttons button:hover{
  opacity: 0.5;
}
.buttons .prev button{
  background: #0090d6;
}
.buttons .play  button{
  background: #0090d6;
}
.buttons .pause  button{
  background: #0090d6;
}
.buttons .next button{
  background: #0090d6;
}
</style>
