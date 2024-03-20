<script setup lang="ts">
import Player from './components/player/MainPlayer.vue'
import {ref,watch} from "vue"
import {io} from "socket.io-client"
import {Howl, Howler} from 'howler';

const player = ref<Howl>()

const socket = io('http://localhost:3000')

socket.emit("play", {
  id: 'watch?=asdsadsa'
})

socket.on("play", (msg) => {
  // alert("playing")
  console.log(msg.info)

  player.value?.off("end")

  player.value = new Howl({
    src: [msg.info],
    html5: true,
    // src: ['https://download.samplelib.com/mp3/sample-9s.mp3']
  });

  console.log("sound", player)

  player.value?.play();

  player.value?.on("end", () => {
    socket.emit("playNext", {})
  })
})

socket.on("pause", (msg) => {
  player.value?.pause()
})

socket.on("resume", (msg) => {
  player.value?.play()
})


// watch(player, (p) => {
//   p?.play();
// }, {deep:true})

// const sound = new Howl({
//   // src: [msg.info]
//   src: ['https://rr4---sn-4pgnuhxqp5-jb3y.googlevideo.com/videoplayback?expire=1710532646&ei=xlP0Ze-hGZeJ4-EP2PWMqAc&ip=139.192.200.165&id=o-AEemJVUqvBJQg88_dmZmyWUzYFvxLhdeMiApOMFbrAVx&itag=251&source=youtube&requiressl=yes&xpc=EgVo2aDSNQ%3D%3D&mh=S0&mm=31%2C26&mn=sn-4pgnuhxqp5-jb3y%2Csn-30a7yney&ms=au%2Conr&mv=m&mvi=4&pl=19&gcr=id&initcwndbps=762500&spc=UWF9f4TR1O9vjYtkARvU-t7acU8sWkBsz80qqeaQsBw2_oI&vprv=1&svpuc=1&mime=audio%2Fwebm&ns=jsQW6atPhOwuedrwspKA-d4Q&gir=yes&clen=1512729&dur=81.221&lmt=1569379367232494&mt=1710510571&fvip=2&keepalive=yes&c=WEB&sefc=1&txp=8301222&n=1Hit_b5vQwja8Q&sparams=expire%2Cei%2Cip%2Cid%2Citag%2Csource%2Crequiressl%2Cxpc%2Cgcr%2Cspc%2Cvprv%2Csvpuc%2Cmime%2Cns%2Cgir%2Cclen%2Cdur%2Clmt&lsparams=mh%2Cmm%2Cmn%2Cms%2Cmv%2Cmvi%2Cpl%2Cinitcwndbps&lsig=APTiJQcwRQIhAJaTK4HSqxcnmb2bIcOPU94j8TfYIALUR-Dizmc1wXLqAiA6LIMQc9QUc25-hHank9HGFTGhG79dGprT0yJlz-WNtA%3D%3D&sig=AJfQdSswRQIhAJEls9n4_wMZayt18O-grMEMTzV_ORe90vrE80_VLenHAiAcR1w7aV9yxWUJkGmqBLlsdn2Z41nbWWnJG-Eeq9HPUg%3D%3D']
// }).play();
</script>

<template>
  <main class="bg-slate-500 min-h-dvh">
    <div class="max-w-md mx-auto">
      <!-- <audio src="https://rr4---sn-4pgnuhxqp5-jb3y.googlevideo.com/videoplayback?expire=1710532646&ei=xlP0Ze-hGZeJ4-EP2PWMqAc&ip=139.192.200.165&id=o-AEemJVUqvBJQg88_dmZmyWUzYFvxLhdeMiApOMFbrAVx&itag=251&source=youtube&requiressl=yes&xpc=EgVo2aDSNQ%3D%3D&mh=S0&mm=31%2C26&mn=sn-4pgnuhxqp5-jb3y%2Csn-30a7yney&ms=au%2Conr&mv=m&mvi=4&pl=19&gcr=id&initcwndbps=762500&spc=UWF9f4TR1O9vjYtkARvU-t7acU8sWkBsz80qqeaQsBw2_oI&vprv=1&svpuc=1&mime=audio%2Fwebm&ns=jsQW6atPhOwuedrwspKA-d4Q&gir=yes&clen=1512729&dur=81.221&lmt=1569379367232494&mt=1710510571&fvip=2&keepalive=yes&c=WEB&sefc=1&txp=8301222&n=1Hit_b5vQwja8Q&sparams=expire%2Cei%2Cip%2Cid%2Citag%2Csource%2Crequiressl%2Cxpc%2Cgcr%2Cspc%2Cvprv%2Csvpuc%2Cmime%2Cns%2Cgir%2Cclen%2Cdur%2Clmt&lsparams=mh%2Cmm%2Cmn%2Cms%2Cmv%2Cmvi%2Cpl%2Cinitcwndbps&lsig=APTiJQcwRQIhAJaTK4HSqxcnmb2bIcOPU94j8TfYIALUR-Dizmc1wXLqAiA6LIMQc9QUc25-hHank9HGFTGhG79dGprT0yJlz-WNtA%3D%3D&sig=AJfQdSswRQIhAJEls9n4_wMZayt18O-grMEMTzV_ORe90vrE80_VLenHAiAcR1w7aV9yxWUJkGmqBLlsdn2Z41nbWWnJG-Eeq9HPUg%3D%3D" autoplay></audio> -->
      <Player />
    </div>
  </main>
</template>
