C<template>
  <div class="container">
    <h3>
      {{ profileData.figure }}
    </h3>
    <div>
      <img
        :src="profileData.picture"
        class="card-img"
      >
    </div>
    <div
      :class="['box-collapse', isCollapsed? 'collapsed': '']"
      @click="toggleBox"
    >
      <div class="ico-align">
        <span class="icon-arrow-bold-down ico-effect" />
      </div>
      <ul>
        <template v-for="item in profileData.list">
          <li :key="item" v-html="item.text" />
        </template>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    profileData: {
      type: Object,
      require: true,
      default: null
    }
  },
  data () {
    return {
      isCollapsed: true
    }
  },
  computed: {
  },
  methods: {
    toggleBox () {
      this.isCollapsed = !this.isCollapsed
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/css/mixins";
@import "~@/css/vars";

.container {
  position: relative;
  margin-top: 3rem;
  margin-bottom: 2rem;
}
.card-img {
  box-shadow: 10px -10px 0px $black;
  shape-outside: url(/profiles/profile.jpg);
  width: 100%;
  object-fit: cover;
  position: absolute;
  left: -1rem;
  top: -1rem;
  z-index: 10;
  max-width: 90px;

  @include breakpoint(medium) {
    max-width: 150px;
  }
}
.box-collapse {
  cursor: pointer;
  border: 2px solid rgba($black, 0.8);
  transition: all 0.25s ease-in-out;
  max-height: 1000px;
  overflow: hidden;
}
.collapsed {
  max-height: 10rem;
  .ico-effect {
    transform: unset;
  }
}
.collapsed::after{
  content: ' ';
  position: absolute;
  bottom: 0.1rem;
  width: 99.4%;
  height: 50%;
  background: rgb(255, 255, 255);
  background: linear-gradient(0deg, rgb(255, 255, 255) 0%, rgba(2,0,36,0) 100%);
    @include breakpoint(medium){
      bottom: 0.1rem;
      width: 99.4%;
    }
}
ul {
  position: relative;
  list-style: outside disc;
  padding: 0;
  margin: 0;
  margin-bottom: 1rem;
  li {
    position: relative;
    left: 2rem;
    padding-right: 2.5rem;
  }
}
h3 {
  margin-left: auto;
  text-align: right;
  padding-bottom: 0.5rem;
  max-width: 50%;
  @include breakpoint(medium) {
    max-width: unset;
  }
}
.ico-align {
  text-align: right;
  margin-top: 1rem;
  margin-right: 1rem;
}
.ico-effect {
  display: inline-block;
  transition: all 0.25s ease-in-out;
  transform: rotate(-180deg);
}
</style>
