<template>
  <div>
    <div class="tab">
      <ul>
        <li :class="{'active':tabTag}" @click="tabTag=true">
          <span>照片库</span>
        </li>
        <li :class="{'active':!tabTag}" @click="tabTag = false">
          <span>视频库</span>
        </li>
      </ul>
    </div>
    <div class="content">
      <div :key="index" class="image-item" v-for="(item,index) in 20" v-show="tabTag">
        <img :src="'../../../static/images/pictures/'+(index+1)+'.jpg'" @click="handleDetial">
        <div class="content-text">
          <p>LANDLORD</p>
          <P>FALL 2019 Menswear</P>
        </div>
      </div>
      <div v-show="!tabTag">
        <div :key="index" class="video-item" v-for="(item,index) in videos">
          <video
            :id="'myVideo'+(index+1)"
            :src="item.src"
            @bindended="handleEnd"
            enable-progress-gesture
            play-btn-position="center"
            poster="../../../static/images/pictures/1.jpg"
            proload="meta"
            title="name"
          ></video>
          <div :hidden="item.click" class="cover">
            <div class="cover-content">
              <img
                @click="handleBegin(item,index+1)"
                src="../../../static/images/pictures/Video.png"
              >
              <span>This is video name</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data() {
    return {
      tabTag: true,
      isHidden: false,
      videos: [
        { src: '../../../static/images/1.mp4', click: false },
        { src: '../../../static/images/2.mp4', click: false },
        { src: '../../../static/images/3.mp4', click: false }
      ]
    }
  },

  onReady() {},

  methods: {
    handleDetial() {
      console.log('=')
      wx.navigateTo({
        url: '/pages/counter/main'
      })
    },
    handleBegin(item, index) {
      const videoContext = wx.createVideoContext('myVideo' + index)
      item.click = true
      videoContext.play()
    },
    handleEnd($event) {
      console.log($event)
    }
  }
}
</script>

<style scoped lang="scss">
.tab {
  ul {
    display: flex;
    li {
      flex: 1;
      text-align: center;
      &.active {
        color: green;
        position: relative;

        span {
          display: inline-block;
          border-bottom: 2px solid green;
        }
      }
    }
  }
}
.content {
  .video-item {
    position: relative;
    margin-bottom: 5px;
    .cover {
      background: #000;
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      .cover-content {
        position: absolute;
        bottom: 10%;
        left: 5%;
        display: flex;
        align-items: center;

        img {
          width: 50px;
          height: 50px;
        }
        span {
          color: #fff;
          margin-left: 5px;
        }
      }
    }
  }
  .image-item {
    width: 49%;
    float: left;
    position: relative;
    img {
      width: 100%;
    }
  }
  .item:nth-child(odd) {
    margin-right: 2%;
  }
  &-text {
    position: absolute;
    color: white;
    margin-left: 10px;
    bottom: 8%;
    left: 5%;
    p:first-child {
      font-size: 13px;
      font-weight: 500;
    }
    p:last-child {
      font-size: 10px;
    }
  }
  video {
    width: 100%;
  }
}
</style>
