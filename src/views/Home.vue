<template>
  <div class="about">
    <div class="search-box">
      <van-search v-model="keywords" placeholder="请输入搜索关键词" show-action @search="onSearch(0)">
        <div slot="action" @click="onSearch(0)">搜索</div>
      </van-search>
    </div>
    <div class="search-songs">
      <van-list v-model="loading" :finished="finished" @load="onLoad">
        <van-cell v-for="(song,index) in songs" :key="song.id+'_'+index" :label="song.artists" @click="addToSongs(song.id)">
          <div slot="title" class="cell-song">
            <div class="song-name">{{song.name}}</div>
            <div class="song-artists">{{song.artists}}</div>
          </div>

          <van-icon slot="right-icon" name="play" class="van-cell__right-icon" />
        </van-cell>
      </van-list>
    </div>
    <aplayer :mini="false" :audio="audio" fixed :volume='0.8' ref="aplayer" :lrcType="1" />

  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "home",
  data() {
    return {
      songs: [],
      loading: false,
      finished: true,
      keywords: "",
      offset: 0,
      songCount: 0,
      audio: []
    };
  },
  components: {},
  mounted() {
    this.init(449818741);
  },
  methods: {
    async onSearch(offset) {
      if (offset === 0) {
        this.offset = 0;
        this.songs = [];
      }
      try {
        const res1 = await axios({
          method: "get",
          url:
            "https://music.zhangyake.site/search?keywords=" +
            this.keywords +
            "&offset=" +
            this.offset
        });

        // console.log(res1.data.result.songs);
        // console.log(res1.data.result.songCount);
        this.songCount = res1.data.result.songCount;

        res1.data.result.songs.forEach(item => {
          this.songs.push({
            id: item.id,
            name: item.name,
            artists:
              item.artists.length > 1
                ? item.artists.reduce((a, b) => {
                    return a.name + "/ " + b.name;
                  })
                : item.artists.length === 1
                  ? item.artists[0].name
                  : ""
          });
        });
        this.offset += 30;
        this.loading = false;
        this.songs.length === this.songCount
          ? (this.finished = true)
          : (this.finished = false);
      } catch (err) {
        console.log(err);
      }
    },
    addToSongs(id) {
      // console.log(id);
      // this.$router.push({ name: "home", params: { id } });
      this.init(id);
    },
    onLoad() {
      this.onSearch(this.offset);
    },
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

        music.id = songId;
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

        const arr = this.audio.filter(item => {
          return +item.id === +songId;
        });
        if (arr && arr.length) {
          this.$refs.aplayer.currentMusic = arr[0];
          this.$refs.aplayer.play();
        } else {
          if (!music.url) {
            this.$toast("歌曲无效!");
          } else {
            this.audio.push(music);
            this.$refs.aplayer.currentMusic = music;
            this.$refs.aplayer.play();
          }
        }
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style lang="less" scoped>
.search-box {
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 1000;
}
.search-songs {
  margin-top: 48px;
  .van-list {
    height: 542px;
    overflow-y: auto;
  }
}
.cell-song {
  width: 300px;
  .song-name {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .song-artists {
    font-size: 12px;
    color: #929292;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
}
</style>
