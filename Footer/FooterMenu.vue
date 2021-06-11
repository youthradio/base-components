<template>
  <div class="top-block">
    <div>
      <ul class="social-menu">
        <li>
          <a
            aria-label="YR Media Youtube"
            href="https://www.youtube.com/user/youthradio"
            target="_blank"
            ><span class="icon-youtube"></span
          ></a>
        </li>
        <li>
          <a
            aria-label="YR Media Facebook"
            href="https://www.facebook.com/yrmediapage"
            target="_blank"
            ><span class="icon-facebook"></span
          ></a>
        </li>
        <li>
          <a
            aria-label="YR Media Twitter"
            href="https://twitter.com/itsYRmedia"
            target="_blank"
            ><span class="icon-twitter"></span
          ></a>
        </li>
        <li>
          <a
            aria-label="YR Media Instagram"
            href="https://www.instagram.com/yr.media"
            target="_blank"
            ><span class="icon-instagram"></span
          ></a>
        </li>
      </ul>
      <p class="copyright">YR Media © 2021</p>
    </div>
    <div>
      <div class="logo">
        <a href="https://yr.media">
          <full-logo />
        </a>
      </div>

      <ul id="menu-footer-menu" class="pages-menu">
        <li
          id="menu-item-36521"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-36521
          "
        >
          <a href="https://yr.media/about-yr/">About YR Media</a>
        </li>
        <li
          id="menu-item-35672"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-35672
          "
        >
          <a href="https://yr.media/donate/">Support Our Work</a>
        </li>
        <li
          id="menu-item-42578"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-42578
          "
        >
          <a href="https://yr.media/career-opportunities/">Careers at YR</a>
        </li>
        <li
          id="menu-item-66507"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-66507
          "
        >
          <a href="https://yr.media/yr-classes/">Apply to Classes</a>
        </li>
        <li
          id="menu-item-43302"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-43302
          "
        >
          <a href="https://yr.media/contact/">Contact Us</a>
        </li>
        <li
          id="menu-item-49761"
          class="
            menu-item
            menu-item-type-post_type
            menu-item-object-page menu-item-49761
          "
        >
          <a href="https://yr.media/privacy-policy/">Privacy Policy</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import FullLogo from './FullLogo.vue'

export default {
  components: {
    FullLogo,
  },
}
</script>

<style scoped lang="scss">
@import '~@/css/mixins';
@import '~@/css/vars';

ul {
  padding: 0;
  margin: 0;
  list-style-type: none;
}
a {
  border-bottom: 0px;
  text-decoration: none;
}

footer {
  padding-top: 1rem;
}

.top-block {
  padding: 50px 30px;
  background-color: $black;

  @include breakpoint(small) {
    display: flex;
    justify-content: space-between;
    padding: 50px 60px;
  }

  & > div {
    @include breakpoint(small) {
      &:last-of-type {
        order: 1;
        display: flex;
      }

      &:first-of-type {
        order: 2;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
      }
    }
  }

  .logo {
    display: none;
    margin-right: 40px;
    a {
      display: block;
      width: 70px;
      height: 70px;
      overflow: hidden;

      .svg-logo {
        transform: scale(1.65);
      }
    }

    @include breakpoint(small) {
      display: block;
    }
  }

  .copyright {
    display: none;
    font: 300 17px/2 'Calps', sans-serif;
    color: $grey;

    @include breakpoint(small) {
      display: block;
    }
  }
}

.pages-menu {
  li {
    font: 900 22px/1.8 'Roboto Mono', sans-serif;
    letter-spacing: 2px;
    text-transform: uppercase;
    a {
      color: $green;

      &:hover {
        color: white;
      }
    }

    @include breakpoint(small) {
      font: 500 19px/1.6 'Roboto Mono', sans-serif;
      letter-spacing: 3px;
    }
  }

  @include breakpoint(medium) {
    column-count: 2;
    column-gap: 40px;
  }

  @include breakpoint(large) {
    column-width: 300px;
  }
}

ul.social-menu {
  display: flex;
  margin-bottom: 20px;
  align-items: center;

  li {
    margin-right: 30px;

    &:last-of-type {
      margin-right: 0;
    }

    a {
      span {
        &:before {
          color: $grey;
          font-size: 24px;
        }

        &.icon-youtube {
          &:before {
            font-size: 20px;
          }
        }

        &:hover {
          &:before {
            color: white;
          }
        }
      }
    }
  }

  @include breakpoint(small) {
    margin-top: 10px;
  }
}

.subscriptions {
  padding: 40px 30px;
  background-color: $green;

  & > div {
    @include breakpoint(large) {
      display: flex;
      justify-content: center;
    }
  }

  .title {
    margin-bottom: 20px;
    color: white;
    font: 700 25px 'Calps', sans-serif;
    letter-spacing: 1.35px;

    @include breakpoint(small) {
      font: 700 57px 'Calps', sans-serif;
      letter-spacing: 0.57px;
    }
    @include breakpoint(large) {
      margin: 0;
      margin-right: 30px;
    }
  }

  .message {
    margin-top: 20px;
    font: 20px 'Roboto Mono', sans-serif;
    color: white;
  }
}
</style>
