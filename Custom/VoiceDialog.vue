<template>
  <div>
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
      <audio>
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
        <img
          :src="guestsMap.get(dialog.speaker).photo.a"
          class="profile-img hidden"
        >
        <img
          :src="guestsMap.get(dialog.speaker).photo.b"
          class="profile-img visible"
        >
        <span class="bio"> Bio </span>
      </div>
      <div
        class="passage"
        :style="{'--border-color': guestsMap.get(dialog.speaker).color}"
      >
        {{ dialog.passage }}
        <div
          class="progress"
          :style="(activePassage === i)? {width: progress}: {}"
        />
      </div>
    </div>
  </div>
</template>

<script>
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
    }
  },
  data () {
    return {
      vueplayer: null,
      activePassage: 0,
      progress: '0%',
      audioDuration: 0
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
  },
  methods: {

    onSeek (event) {
      // find active live when audion seeking
      const currTime = this.vueplayer.player.currentTime
      this.dialogs.map((e, i) => {
        const start = e.startSeconds
        const end = e.endSeconds
        if (currTime > start && currTime <= end) {
          this.activePassage = i
          // this.scrollTo(this.activePassage)
        }
      })
      // console.log(event)
    },
    onAudioPlay (event) {
      // console.log(event)
    },
    onAudioPause (event) {
      // console.log(event)
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
      // console.log(event)
    },
    audioReady (event) {
      this.audioDuration = this.vueplayer.player.duration
      // console.log(event)
    }

  }
}
</script>

<style lang="scss" scoped>
.dialog {
  display: flex;
}
.profile-container {
  position: relative;
  display: flex;
  flex-direction: column;
  // background-color: lightblue;

  .profile-img {
    width: 100px;
    height: auto;
  }
  .hidden {
    display: none;
  }
  &:hover {
    .visible {
      display: none;
    }
    .hidden {
      display: inline-block;
    }
  }
  .bio {
    font-size: 1rem;
    font-weight: 200;
    text-align: center;
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
  margin-bottom: 1rem;
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
}
.player-custom-style >>> .plyr--audio .plyr__controls {
  background: none;
}
</style>
