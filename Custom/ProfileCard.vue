C<template>
  <div class="container">
    <div class="head-profile">
      <img
        :src="profileData.picture"
        class="card-img"
      >
      <h3>
        {{ profileData.figure }}
      </h3>
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
          <li
            :key="item"
            v-html="item.text"
          />
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
  margin-bottom: 1rem;
}
.head-profile {
  display: flex;
  align-items: flex-end;
}
.card-img {
  box-shadow: 0px 10px 0px rgba($black, 0.8);
  shape-outside: url(/profiles/profile.jpg);
  width: 100%;
  object-fit: cover;
  margin-bottom: -1rem;
  margin-left: -1rem;
  z-index: 10;
  max-width: 90px;
  border-radius: 100%;
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
.collapsed::after {
  content: " ";
  position: absolute;
  bottom: 0.1rem;
  width: 99%;
  height: 50%;
  background: rgb(255, 255, 255);
  background: linear-gradient(
    0deg,
    rgb(255, 255, 255) 0%,
    rgba(2, 0, 36, 0) 100%
  );
  background-image: linear-gradient(to bottom, rgba(255, 255, 255, 0) 0%,rgba(255, 255, 255, 1) 100%); //safari fix
  @include breakpoint(medium) {
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
  max-width: 50%;
  padding-bottom: 0.5rem;
  margin-left: 1rem;
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
