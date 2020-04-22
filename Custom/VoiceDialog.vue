<template>
  <div ref="container">
    <VuePlyr
      ref="audioPlayer"
      :options="playerOptions"
      :emit="['play','pause','timeupdate','ready','canplay','seeking']"
      @seeking="onSeek"
      @play="onAudioPlay"
      @pause="onAudioPause"
      @timeupdate="onTime"
      @ready="onPlayerReady"
      @canplay="audioReady"
    >
      <audio preload="metadata">
        <source
          v-for="audio in audios"
          :key="audio.src"
          :src="audio.src"
          :type="audio.format"
        >
      </audio>
    </VuePlyr>

    <div
      v-for="(dialog, i) in dialogs"
      :key="dialog.passage"
      class="dialog"
    >
      <div class="profile-container">
        <template v-if="!dialog.repeate">
          <img
            :data-src="guestsMap.get(dialog.speaker).photo.a"
            width="200px"
            height="200px"
            class="lazyload profile-img hidden"
          >
          <img
            :data-src="guestsMap.get(dialog.speaker).photo.b"
            width="200px"
            height="200px"
            class="lazyload profile-img visible"
          >
          <span class="bio"> Bio </span>
        </template>
        <template v-else>
          <div class="profile-img" />
        </template>
        <div
          class="bio-tootlip"
          :style="{backgroundColor: guestsMap.get(dialog.speaker).color}"
        >
          <strong> {{ guestsMap.get(dialog.speaker).name }} </strong>
          <span v-html="guestsMap.get(dialog.speaker).bio" />
        </div>
      </div>
      <div
        class="passage"
        :style="{'--border-color': guestsMap.get(dialog.speaker).color}"
      >
        <div class="small-play">
          <a
            href="#"
            @click.prevent="togglePassage(i)"
          >
            <svg
              width="20"
              height="20"
              viewBox="0 0 512 512"
            >
              <path
                v-if="(activePassage === i) && isPlaying"
                style="fill:black;"
                d="M256 8C119 8 8 119 8 256s111 248 248 248 248-111 248-248S393 8 256 8zm0 448c-110.5 0-200-89.5-200-200S145.5 56 256 56s200 89.5 200 200-89.5 200-200 200zm96-280v160c0 8.8-7.2 16-16 16h-48c-8.8 0-16-7.2-16-16V176c0-8.8 7.2-16 16-16h48c8.8 0 16 7.2 16 16zm-112 0v160c0 8.8-7.2 16-16 16h-48c-8.8 0-16-7.2-16-16V176c0-8.8 7.2-16 16-16h48c8.8 0 16 7.2 16 16z"
                class=""
              />
              <path
                v-else
                style="fill:black;"
                d="M371.7 238l-176-107c-15.8-8.8-35.7 2.5-35.7 21v208c0 18.4 19.8 29.8 35.7 21l176-101c16.4-9.1 16.4-32.8 0-42zM504 256C504 119 393 8 256 8S8 119 8 256s111 248 248 248 248-111 248-248zm-448 0c0-110.5 89.5-200 200-200s200 89.5 200 200-89.5 200-200 200S56 366.5 56 256z"
                class=""
              /></svg>
          </a>
          <a
            href="#"
            @click.prevent="tweetMessage(dialog.passage, guestsMap.get(dialog.speaker))"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="18"
              height="18"
              viewBox="0 0 24 24"
            >
              <path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z" /></svg>
          </a>
        </div>
        <div class="margin-right">
          {{ dialog.passage }}
          <h5 class="speaker-name">
            {{ guestsMap.get(dialog.speaker).name }}
          </h5>
        </div>
        <div
          class="progress"
          :style="(activePassage === i)? {width: progress}: {}"
        />
      </div>
    </div>
  </div>
</template>

<script>
import POSTCONFIG from '../../post.config'
import VuePlyr from './VuePlyr.vue'

export default {
  components: { VuePlyr },
  props: {
    audios: {
      type: Array,
      require: true,
      default: null
    },
    guests: {
      type: Array,
      require: true,
      default: null
    },
    dialogs: {
      type: Array,
      require: true,
      default: null
    },
    sectionId: {
      type: String,
      require: true,
      default: null
    }
  },
  data () {
    return {
      vueplayer: null,
      activePassage: 0,
      progress: '0%',
      audioDuration: 0,
      isPlaying: false
    }
  },
  computed: {
    guestsMap () {
      return new Map(this.guests.map(g => [g.key, g]))
    },
    playerOptions () {
      return {
        iconUrl: process.env.baseUrl + '/images/plyr.svg',
        volume: 1,
        controls: [
          'play-large', // The large play button in the center
          // 'restart', // Restart playback
          // 'rewind', // Rewind by the seek time (default 10 seconds)
          'play', // Play/pause playback
          // 'fast-forward', // Fast forward by the seek time (default 10 seconds)
          'progress', // The progress bar and scrubber for playback and buffering
          'current-time', // The current time of playback
          // 'duration', // The full duration of the media
          'mute', // Toggle mute
          'volume', // Volume control
          'pip', // Picture-in-picture (currently Safari only)
          'airplay' // Airplay (currently Safari only)
          // 'settings' // Settings menu
        ]
      }
    }

  },
  mounted () {
    this.vueplayer = this.$refs.audioPlayer
    const observer = new IntersectionObserver((entries, observer) => {
      entries.forEach((entry) => {
        if (entry.intersectionRatio <= 0 && this.vueplayer.player.playing) {
          this.vueplayer.player.pause()
        }
      })
    },
    {
      threshold: 0
    })
    observer.observe(this.$refs.container)
  },
  methods: {
    tweetMessage (msg, author) {
      const url = POSTCONFIG.url + '/' + this.sectionId
      const tweet = `#InTheBlackMirror: “${msg.replace(/(\r\n|\n|\r)/gm, '')}” by ${author.name} @${author.twitter} - via @itsyrmedia ${url}`
      const tweetUrl = `https://twitter.com/intent/tweet?text=${encodeURIComponent(tweet)}`
      window.open(tweetUrl, 'pop', 'width=600, height=400, scrollbars=no')
    },
    togglePassage (id) {
      const start = this.dialogs[id].startSeconds
      if (this.activePassage === id && this.isPlaying) {
        this.vueplayer.player.pause()
        return
      }
      this.vueplayer.player.currentTime = start
      this.vueplayer.player.play()
    },
    onSeek (event) {
      this.setCurrPassage()
    },
    onAudioPlay (event) {
      this.isPlaying = true
    },
    onAudioPause (event) {
      this.isPlaying = false
    },
    onTime (event) {
      const currTime = this.vueplayer.player.currentTime
      const start = this.dialogs[this.activePassage].startSeconds
      const end = this.dialogs[this.activePassage].endSeconds
      this.progress = (100 * (currTime - start) / (end - start)) + '%'
      if (currTime >= end) {
        this.progress = '0%'
        this.activePassage = (this.activePassage + 1) % this.dialogs.length
      }
    },
    onPlayerReady (event) {
    },
    audioReady (event) {
      this.audioDuration = this.vueplayer.player.duration
    },
    setCurrPassage () {
      const currTime = this.vueplayer.player.currentTime
      this.dialogs.map((e, i) => {
        const start = e.startSeconds
        const end = e.endSeconds
        if (currTime >= start && currTime < end) {
          this.activePassage = i
        }
      })
    }

  }
}
</script>

<style lang="scss" scoped>
@import "~@/css/mixins";

.dialog {
  display: flex;
  align-items: flex-start;
  margin-top: 1rem;
}
.profile-container {
  position: sticky;
  top: 130px;
  display: flex;
  flex-direction: column;
  // background-color: lightblue;
  .profile-img {
    width: 60px;
    @include breakpoint(medium) {
      width: 100px;
    }
    height: auto;
  }
  .hidden {
    display: none;
  }
  &:hover {
    z-index: 10;
    .visible {
      display: none;
    }
    .hidden {
      display: inline-block;
    }
  }

  .bio {
    background-color: white;
    font-size: 0.5rem;
    font-weight: 200;
    text-align: center;
    width: 100%;
    cursor: pointer;
    &:hover {
      + .bio-tootlip {
        display: inline-block;
      }
    }
  }
  .bio-tootlip {
    padding: 0.8em;
    pointer-events: none;
    display: none;
    position: absolute;
    font-size: 0.8rem;
    top: 50px;
    left: 50%;
    right: MIN(-200px, -50vw);
  }
}

.passage {
  --border-color: red;
  position: relative;
  border-bottom: var(--border-color);
  border-bottom-width: 2px;
  border-bottom-style: solid;
  border-left: var(--border-color);
  border-left-width: 2px;
  border-left-style: solid;
  margin-left: 1rem;
  padding: 0.5rem;
  &:before,
  &:after {
    right: 100%;
    top: 20%;
    border: solid transparent;
    content: " ";
    height: 0;
    width: 0;
    position: absolute;
    pointer-events: none;
  }
  &:after {
    border-right-color: white;
    border-width: 14px;
    margin-top: -14px;
  }
  &:before {
    border-right-color: var(--border-color);
    border-width: 17px;
    margin-top: -17px;
  }
  .progress {
    position: absolute;
    background-color: var(--border-color);
    margin-left: -0.5rem;
    height: 5px;
    bottom: 0;
  }
  .small-play {
    position: sticky;
    top: 130px;
    float: right;
    display: flex;
    flex-direction: column;
    place-items: center;
    a {
      text-decoration: unset;
      border-bottom: unset;
      display: block;
    }
    a:hover {
      background-color: unset;
      text-decoration: unset;
    }
  }
  .margin-right {
    margin-right: 25px;
  }
  .speaker-name {
    padding: 0;
    font-weight: bold;
  }
}
.player-custom-style >>> .plyr--audio .plyr__controls {
  background: none;
}
</style>
