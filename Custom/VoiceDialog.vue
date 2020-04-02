<template>
  <div>
    <VuePlyr
      ref="audioPlayer"
      :options="playerOptions"
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
      v-for="dialog in dialogs"
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
      <div class="passage">
        {{ dialog.passage }}
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

  methods: {

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
  position: relative;
  border-bottom: lightblue;
  border-bottom-width: 2px;
  border-bottom-style: solid;
  border-left: lightblue;
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
    border-right-color: lightblue;
    border-width: 17px;
    margin-top: -17px;
  }
}
</style>
