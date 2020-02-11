<template>
  <div id="app">
    <header>
    <h1>My Music</h1>
    </header>

    <main>
    <section class="player">
    <h2 class="song-title">{{current.title}}-<span>{{current.artist}}</span></h2>

    
    </section>
    <section class="playlist">
   

  <!-- <div class="col-lg-2" v-for="pic in pics" :key="pic.src">
  <img :src="getImage(pic)" v-bind:alt="pic">
</div> -->
    <div class="songImageDiv" >
      <img :src="getImage()" class="songImage">
      </div>
      
      <div class="controls">
    <button class="prev" @click="prev"><i class="fa fa-backward"></i></button>
    <button class="play" v-if="!isPlaying" @click="play"><i class="fa fa-play"></i></button>
    <button class="pause" v-else @click="pause"><i class="fa fa-pause"></i></button>
    <button class="next" @click="next"><i class="fa fa-forward"></i></button>
    </div>

    <button v-for="song in songs" :key="song.src" @click="play(song)" 
    :class="(song.src==current.src)?'song playing':'song'">
    {{song.title}} - {{song.artist}}
    </button>
    </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      current:{},
      index:0,
      isPlaying:false,
      songs:[
        {
        title:'Combination',
        artist:'Amrit Maan',
        src:require('./assets/Combination.mp3'),
        image:require('./assets/combination.jpg')
      },
      {
        title:'Intentions',
        artist:'Quavo',
        src:require('./assets/Intentions.mp3'),
        image:require('./assets/intentions.jpg')
      },
      {
        title:'Na Ja Tu',
        artist:'Dhvani Bhanushali',
        src:require('./assets/Najatu.mp3'),
        image:require('./assets/najatu.jpg')
      }
      ],
      // pics:[
      //   {
      //   title:'Combination',
      //   artist:'Amrit Maan',
      //   src:require('./assets/combination.jpg')
      // },
      // {
      //   title:'Intentions',
      //   artist:'Quavo',
      //   src:require('./assets/intentions.jpg')
      // },
      // {
      //   title:'Na Ja Tu',
      //   artist:'Dhvani Bhanushali',
      //   src:require('./assets/najatu.jpg')
      // }

      // ],
      player:new Audio()

    }
  },
  methods:{
    play(song){
      if(typeof song.src != "undefined"){
        this.current=song;
        this.player.src=this.current.src;
      }
      this.player.play();
      this.isPlaying=true;
    },
    pause(){
      this.player.pause();
      this.isPlaying=false;
    },
    next(){
        this.index++;
        if(this.index>this.songs.length-1){
          this.index=0;
        }
        this.current=this.songs[this.index];
        this.play(this.current);
    },
    prev(){
         this.index--;
        if(this.index<0){
          this.index=this.songs.length-1;
        }
        this.current=this.songs[this.index];
        this.play(this.current);
    },
     getImage() {
       return this.current.image;
     }
},

 created(){
     this.current=this.songs[this.index];
     this.player.src=this.current.src;
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}
body{
  font-family:sans-serif;
}
header{
  display:flex;
  justify-content:center;
  align-items:center;
  padding:15px;
  background-color:#212121;
  color:#FFF;
}
main{
  width:100%;
  max-width:768px;
  margin:0 auto;
  padding:25px;
}
.song-title{
  color:#212121;
  font-size:32px;
  font-weight:700;
  text-transform:uppercase;
  text-align:center;
}

.song-title span{
  font-weight:400;
  font-style:italic;
}

.controls{
  display:flex;
  justify-content:center;
  align-items:center;
  padding:30 px 15px;
}

button{
  appearance:none;
  background:none;
  border:none;
  outline:none;
  cursor:pointer;
}
button:hover{
  opacity:0.8;
}

.play, .pause{
    font-size: 20px;
    padding: 15px 25px;
    border-radius: 50%; 
    margin: 10px 35px;
    color: #FFF;
    background-color: #b30000;
}

.next, .prev{
   font-size:16px;
   padding:10px 20px;
   border-radius:50%;
   color:#FFF;
   background-color:#0000b3
}

.playlist{
  padding:0px 30px;
}

.playlist h3{
  color:#212121;
  font-size:28px;
  font-weight:400;
  margin:30px 15px;
  text-align:center;
}

.playlist .song{
  display:block;
  width:100%;
  padding:15px;
  font-size:20px;
  font-weight:700;
  cursor:pointer;
}

.playlist .song:hover{
color:#FF5858;
}

.playlist .song.playing{
  color:#FFF;
  background-image:linear-gradient(to right,#CC2E5D,#FF5858);
}
.songImageDiv{
    margin: 15px 0;
    text-align: center
}


.songImage{
  width:100%;
  height:300px;
  border-radius: 50%;
}
</style>
