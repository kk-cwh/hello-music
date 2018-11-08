<template>
  <div class="home">
    <aplayer :audio="audio"   :volume='0.8' ref="aplayer" :lrcType="1" />

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "home",
  components: {},
  data() {
    return {
      list: [
        {
          title: "secret base~君がくれたもの~",
          artist: "Silent Siren",
          src:
            "http://m10.music.126.net/20181108144150/311a2e1871b3040b9c30b18c59ae14e2/ymusic/603f/2799/ea87/0ac26d0e219c049b2c5a12fd6be2826f.mp3",
          pic: "https://moeplayer.b0.upaiyun.com/aplayer/secretbase.jpg",

          lrc:
            "[00:00.00] 作曲 : 黄家驹 [00:01.00] 作词 : 黄家驹 [00:17.88]今天我 [00:21.27]寒夜里看雪飘过 [00:24.34]怀著冷却了的心窝飘远方 [00:30.18]风雨里追赶 [00:33.36]雾里分不清影踪 [00:36.42]天空海阔你与我 [00:39.38]可会变 (三子:谁没在变) [00:42.86]多少次 [00:45.97]迎著冷眼与嘲笑 [00:49.22]从没有放弃过心中的理想 [00:55.11]一刹那恍惚 [00:58.34]若有所失的感觉 [01:01.48]不知不觉已变淡 [01:04.46]心里爱 (三子:谁明白我) [01:08.17]原谅我这一生不羁放纵爱自由 [01:14.79]也会怕有一天会跌倒 Hoo No [01:21.20]背弃了理想 [01:23.42]谁人都可以 [01:26.98]那会怕有一天只你共我 [01:41.84]今天我 [01:45.44]寒夜里看雪飘过 [01:48.79]怀著冷却了的心窝飘远方 [01:53.99]风雨里追赶 [01:57.76]雾里分不清影踪 [02:00.89]天空海阔你与我 [02:03.87]可会变 (三子:谁没在变) [02:07.22]原谅我这一生不羁放纵爱自由 [02:14.0]也会怕有一天会跌倒 Hoo No [02:20.56]背弃了理想 [02:22.77]谁人都可以 [02:26.61]那会怕有一天只你共我 Oh Yeah [03:07.24]仍然自由自我 [03:10.96]永远高唱我歌 [03:14.34]走遍千里 [03:18.61]原谅我这一生不羁放纵爱自由 [03:24.86]也会怕有一天会跌倒 Hoo No [03:31.52]背弃了理想 [03:33.86]谁人都可以 [03:37.20]那会怕有一天只你共我 [03:44.5]背弃了理想 [03:46.86]谁人都可以 [03:50.66]那会怕有一天只你共我 Oh Yeah [03:56.77](三子：)原谅我这一生不羁放纵爱自由 (Oh Yeah) [04:03.58]也会怕有一天会跌倒 (Oh…) [04:08.77]背弃了理想 [04:11.81]谁人都可以 (Woo…) [04:15.70]那会怕有一天只你共我 "
        }
      ],
      audio: [
        // {
        //   name: "I Really Like You 西班牙语版（Cover Carly Rae Jepsen）",
        //   artist: "熊子",
        //   url: "http://pdacsgxq7.bkt.clouddn.com/mp3/mucho.mp3",
        //   cover: 'http://p1.music.126.net/UhbkP71d9KTMsdNczCf2wA==/109951162986700564.jpg?param=300y300', // prettier-ignore
        //   lrc: "http://pdacsgxq7.bkt.clouddn.com/lrc/mucho.lrc"
        // }
        // {
        //   name: "Mermaid girl (Extended RRver.)",
        //   artist: "森永真由美",
        //   url: "http://pdacsgxq7.bkt.clouddn.com/mp3/mermaidgirl.mp3",
        //   cover: 'http://p1.music.126.net/xXxBuZksld5HtovQxI1D0A==/3227066630258578.jpg?param=300y300', // prettier-ignore
        //   lrc: "http://pdacsgxq7.bkt.clouddn.com/lrc/mermaidgirl.lrc"
        // },
        // {
        //   name: "ヒビカセ",
        //   artist: "れをる",
        //   url: "http://pdacsgxq7.bkt.clouddn.com/mp3/hibikase.mp3",
        //   cover: 'http://p1.music.126.net/cZPx3peGTuWEI_GaZB5CDg==/8892850045794893.jpg?param=300y300', // prettier-ignore
        //   lrc: "http://pdacsgxq7.bkt.clouddn.com/lrc/hibikase.lrc"
        // }
      ],
      music: {
        title: "secret base~君がくれたもの~",
        artist: "Silent Siren",
        src:
          "http://m10.music.126.net/20181108144150/311a2e1871b3040b9c30b18c59ae14e2/ymusic/603f/2799/ea87/0ac26d0e219c049b2c5a12fd6be2826f.mp3",
        pic: "https://moeplayer.b0.upaiyun.com/aplayer/secretbase.jpg",

        lrc:
          "[00:00.00] 作曲 : 黄家驹 [00:01.00] 作词 : 黄家驹 [00:17.88]今天我 [00:21.27]寒夜里看雪飘过 [00:24.34]怀著冷却了的心窝飘远方 [00:30.18]风雨里追赶 [00:33.36]雾里分不清影踪 [00:36.42]天空海阔你与我 [00:39.38]可会变 (三子:谁没在变) [00:42.86]多少次 [00:45.97]迎著冷眼与嘲笑 [00:49.22]从没有放弃过心中的理想 [00:55.11]一刹那恍惚 [00:58.34]若有所失的感觉 [01:01.48]不知不觉已变淡 [01:04.46]心里爱 (三子:谁明白我) [01:08.17]原谅我这一生不羁放纵爱自由 [01:14.79]也会怕有一天会跌倒 Hoo No [01:21.20]背弃了理想 [01:23.42]谁人都可以 [01:26.98]那会怕有一天只你共我 [01:41.84]今天我 [01:45.44]寒夜里看雪飘过 [01:48.79]怀著冷却了的心窝飘远方 [01:53.99]风雨里追赶 [01:57.76]雾里分不清影踪 [02:00.89]天空海阔你与我 [02:03.87]可会变 (三子:谁没在变) [02:07.22]原谅我这一生不羁放纵爱自由 [02:14.0]也会怕有一天会跌倒 Hoo No [02:20.56]背弃了理想 [02:22.77]谁人都可以 [02:26.61]那会怕有一天只你共我 Oh Yeah [03:07.24]仍然自由自我 [03:10.96]永远高唱我歌 [03:14.34]走遍千里 [03:18.61]原谅我这一生不羁放纵爱自由 [03:24.86]也会怕有一天会跌倒 Hoo No [03:31.52]背弃了理想 [03:33.86]谁人都可以 [03:37.20]那会怕有一天只你共我 [03:44.5]背弃了理想 [03:46.86]谁人都可以 [03:50.66]那会怕有一天只你共我 Oh Yeah [03:56.77](三子：)原谅我这一生不羁放纵爱自由 (Oh Yeah) [04:03.58]也会怕有一天会跌倒 (Oh…) [04:08.77]背弃了理想 [04:11.81]谁人都可以 (Woo…) [04:15.70]那会怕有一天只你共我 "
      }
    };
  },
  mounted() {
    // setTimeout(() => {
    //   this.$refs.aplayer.play();
    // }, 10000);
    var songId = this.$route.params.id ? this.$route.params.id : "554191055";
    this.init(songId);
  },
  methods: {
    async init(songId) {
      try {
        let music = {};
        const res1 = await axios({
          method: "get",
          url: "https://music.zhangyake.site/music/url?id=" + songId
        });
        const res2 = await axios({
          method: "get",
          url: "https://music.zhangyake.site/lyric?id=" + songId
        });
        const res3 = await axios({
          method: "get",
          url: "https://music.zhangyake.site/song/detail?ids=" + songId
        });

        music.url = res1.data.data[0].url;
        music.artist =
          res3.data.songs[0].ar.length > 1
            ? res3.data.songs[0].ar.reduce((a, b) => {
                return a.name + " / " + b.name;
              })
            : res3.data.songs[0].ar.length === 1
              ? res3.data.songs[0].ar[0].name
              : "";
        music.cover = res3.data.songs[0].al.picUrl;
        music.name = res3.data.songs[0].name;
        music.lrc = res2.data.lrc.lyric;
        this.audio.push(music);
        console.log(res2.data);
        console.log(res3.data.songs[0]);
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>
