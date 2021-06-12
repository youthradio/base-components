<template>
  <div
    :class="[
      'top-header header-sticky row',
      activeMenu ? 'navigation-open' : '',
    ]"
    :style="
      menuFixed ? { position: 'sticky', top: 0 } : { position: 'initial' }
    "
  >
    <header
      class="main-header"
      tabindex="-1"
      :style="hideNavbar && !menuFixed ? { top: '-68px' } : {}"
    >
      <div class="header-container mobile">
        <div>
          <div class="logo-menu-wrapper">
            <div class="logo prod">
              <a
                aria-label="YR Media Home"
                tabindex="0"
                href="https://yr.media"
              >
                <!--?xml version="1.0" encoding="UTF-8"?-->
                <svg
                  alt="YR Media Logo"
                  width="66px"
                  height="66px"
                  viewBox="0 0 66 66"
                  version="1.1"
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                >
                  <!-- Generator: Sketch 51.2 (57519) - http://www.bohemiancoding.com/sketch -->
                  <title>YR logo Copy</title>
                  <desc>Created with Sketch.</desc>
                  <defs></defs>
                  <g
                    id="homepage"
                    stroke="none"
                    stroke-width="1"
                    fill="none"
                    fill-rule="evenodd"
                  >
                    <g
                      id="homepage-DESKTOP"
                      transform="translate(-35.000000, -41.000000)"
                      fill="#FFFFFF"
                    >
                      <g id="Group" transform="translate(-2.000000, 0.000000)">
                        <g
                          id="YR-logo"
                          transform="translate(37.000000, 41.000000)"
                        >
                          <path
                            id="Fill-1"
                            d="M61.3306229,0 L58.5102548,0 C56.731012,0 55.1779931,1.00390191 54.3907504,2.46972188 C54.2448195,2.74194559 54.0786605,3.23137344 53.8852555,3.48594161 C53.3605647,4.17717632 52.340493,4.70376291 50.8539377,4.70376291 C49.1376496,4.70376291 48.1318201,3.86471442 47.7445974,2.8474682 L47.7445974,2.85198474 C47.0238183,1.20755645 45.3733745,0.0494765564 43.4622366,0.0494765564 L40.6420748,0.0494765564 C38.0739381,0.0494765564 35.9726978,2.13939915 35.9726978,4.69370336 L35.9726978,14.5670479 C35.9611389,15.9398683 34.6198953,17.608727 33.2152842,17.608727 C33.1628564,17.608727 33.1114607,17.6013363 33.0596521,17.5974356 L33.0596521,17.597025 C31.5840365,17.4798005 30.5458008,15.7154788 30.3395986,14.0954809 C30.331755,14.03266 30.3228795,13.996733 30.3168936,13.9519783 C30.0138857,11.6834474 28.0480494,9.91850983 25.6879726,9.91850983 L22.8676045,9.91850983 C20.2994677,9.91850983 18.1982274,12.0082271 18.1982274,14.5627366 L18.1982274,32.283761 L18.187907,33.5182113 C18.0919269,35.2689834 16.7766908,37.1088544 15.1780556,37.1088544 C13.5177042,37.1088544 12.1591223,35.1240438 12.1591223,33.3155833 L12.1591223,29.4141207 L12.1591223,14.5711538 L12.1591223,14.5627366 C12.1591223,12.0082271 10.057882,9.91850983 7.48974524,9.91850983 L4.66937708,9.91850983 C2.10124033,9.91850983 0,12.0082271 0,14.5627366 L0,20.1958787 L0,24.0973412 L0,36.5011755 L0,38.9405135 L0,38.9489306 C0,41.5030295 2.10124033,43.5931574 4.66937708,43.5931574 L7.48974524,43.5931574 C8.2404536,43.5931574 8.98620815,43.4100326 9.65043127,43.061849 C10.2971097,42.7229038 10.8608117,42.2322442 11.2860136,41.6407838 C11.4439163,41.4215267 11.5826229,41.1883094 11.699863,40.9448272 C11.8495093,40.6352395 11.9258805,40.3188769 12.1578839,40.0530174 C12.3574811,39.8241114 12.6026946,39.6069072 12.8633887,39.4492392 C13.1740338,39.2611872 13.5164658,39.1279495 13.8681862,39.0388507 C14.2851317,38.9333281 14.7165258,38.8895998 15.1462687,38.8895998 C16.8623504,38.8895998 18.1784122,40.521505 18.1784122,41.4153678 C18.1784122,41.6206647 18.1982274,63.2162577 18.1982274,63.2162577 C18.1982274,68.6194672 30.3573497,66.3837838 30.3573497,54.5143374 L30.3573497,49.6011716 L30.3573497,49.600761 L30.3573497,40.0916133 L30.3573497,37.9591942 L30.360033,22.5036213 C30.360033,20.7705047 31.7130419,19.3465653 33.0596521,19.2276984 L33.0596521,19.2279037 C33.1114607,19.2235925 33.1628564,19.2153806 33.2152842,19.2153806 C34.6198953,19.2153806 35.9611389,20.851597 35.9726978,22.4633831 L35.9716657,31.9947029 L35.9726978,31.9947029 L35.9726978,32.0004513 C35.9726978,34.5547555 38.0739381,36.6446781 40.6420748,36.6446781 L43.4622366,36.6446781 C46.0305798,36.6446781 48.1318201,34.5547555 48.1318201,32.0004513 L48.1318201,14.370784 L48.1318201,11.3406016 L48.1318201,10.0767938 C48.1318201,7.797998 49.2231028,6.48430305 50.8219444,6.48430305 C52.4544306,6.48430305 53.7919588,8.40239212 53.8367495,10.1853958 C53.8381944,11.5514415 53.8462443,17.1808882 53.8462443,17.1808882 C53.8462443,19.7544903 56.0816503,19.9606084 58.4941549,19.9606084 C60.2486286,19.9606084 62.2516184,19.2482281 63.7344584,17.4426418 C65.020178,15.8770475 66,14.5452864 66,11.0835698 L66,7.56457541 L66,7.09198191 L66,4.69370336 L66,4.65264397 L66,4.6442268 C66,2.09012789 63.8987597,0 61.3306229,0"
                          ></path>
                        </g>
                      </g>
                    </g>
                  </g>
                </svg>
              </a>
            </div>
            <button
              tabindex="0"
              :aria-checked="activeMenu"
              aria-label="Open menu"
              class="hamburger"
              @click="toggleMenu()"
            >
              <span></span>
              <span></span>
              <span></span>
              <span></span>
            </button>
          </div>
          <div
            class="mobile-flex-right btns-wrp"
            style="justify-content: flex-end"
          >
            <!-- <a
              href="https://adp.fm/"
              class="adp-fm-link desktop ellipsis"
              target="_blank"
              ><span class="blinking-red"></span>Live on ADP.FM: SZA
            </a>
            <a href="https://adp.fm/" class="adp-fm-link mobile" target="_blank"
              ><span class="blinking-red"></span>Live: ADP.FM</a
            > -->
            <a
              href="https://yr.media/yr-media-community/"
              class="get-involved desktop"
              target="_blank"
              >Get Involved</a
            >
            <a
              href="https://yr.media/yr-media-community/"
              class="get-involved mobile"
              target="_blank"
              >Get Involved</a
            >
          </div>
        </div>
      </div>
      <div class="header-container desktop">
        <div>
          <div class="logo prod">
            <a aria-label="YR Media Home" href="https://yr.media">
              <!--?xml version="1.0" encoding="UTF-8"?-->
              <svg
                alt="YR Media Logo"
                width="66px"
                height="66px"
                viewBox="0 0 66 66"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink"
              >
                <!-- Generator: Sketch 51.2 (57519) - http://www.bohemiancoding.com/sketch -->
                <title>YR logo Copy</title>
                <desc>Created with Sketch.</desc>
                <defs></defs>
                <g
                  id="homepage"
                  stroke="none"
                  stroke-width="1"
                  fill="none"
                  fill-rule="evenodd"
                >
                  <g
                    id="homepage-DESKTOP"
                    transform="translate(-35.000000, -41.000000)"
                    fill="#FFFFFF"
                  >
                    <g id="Group" transform="translate(-2.000000, 0.000000)">
                      <g
                        id="YR-logo"
                        transform="translate(37.000000, 41.000000)"
                      >
                        <path
                          id="Fill-1"
                          d="M61.3306229,0 L58.5102548,0 C56.731012,0 55.1779931,1.00390191 54.3907504,2.46972188 C54.2448195,2.74194559 54.0786605,3.23137344 53.8852555,3.48594161 C53.3605647,4.17717632 52.340493,4.70376291 50.8539377,4.70376291 C49.1376496,4.70376291 48.1318201,3.86471442 47.7445974,2.8474682 L47.7445974,2.85198474 C47.0238183,1.20755645 45.3733745,0.0494765564 43.4622366,0.0494765564 L40.6420748,0.0494765564 C38.0739381,0.0494765564 35.9726978,2.13939915 35.9726978,4.69370336 L35.9726978,14.5670479 C35.9611389,15.9398683 34.6198953,17.608727 33.2152842,17.608727 C33.1628564,17.608727 33.1114607,17.6013363 33.0596521,17.5974356 L33.0596521,17.597025 C31.5840365,17.4798005 30.5458008,15.7154788 30.3395986,14.0954809 C30.331755,14.03266 30.3228795,13.996733 30.3168936,13.9519783 C30.0138857,11.6834474 28.0480494,9.91850983 25.6879726,9.91850983 L22.8676045,9.91850983 C20.2994677,9.91850983 18.1982274,12.0082271 18.1982274,14.5627366 L18.1982274,32.283761 L18.187907,33.5182113 C18.0919269,35.2689834 16.7766908,37.1088544 15.1780556,37.1088544 C13.5177042,37.1088544 12.1591223,35.1240438 12.1591223,33.3155833 L12.1591223,29.4141207 L12.1591223,14.5711538 L12.1591223,14.5627366 C12.1591223,12.0082271 10.057882,9.91850983 7.48974524,9.91850983 L4.66937708,9.91850983 C2.10124033,9.91850983 0,12.0082271 0,14.5627366 L0,20.1958787 L0,24.0973412 L0,36.5011755 L0,38.9405135 L0,38.9489306 C0,41.5030295 2.10124033,43.5931574 4.66937708,43.5931574 L7.48974524,43.5931574 C8.2404536,43.5931574 8.98620815,43.4100326 9.65043127,43.061849 C10.2971097,42.7229038 10.8608117,42.2322442 11.2860136,41.6407838 C11.4439163,41.4215267 11.5826229,41.1883094 11.699863,40.9448272 C11.8495093,40.6352395 11.9258805,40.3188769 12.1578839,40.0530174 C12.3574811,39.8241114 12.6026946,39.6069072 12.8633887,39.4492392 C13.1740338,39.2611872 13.5164658,39.1279495 13.8681862,39.0388507 C14.2851317,38.9333281 14.7165258,38.8895998 15.1462687,38.8895998 C16.8623504,38.8895998 18.1784122,40.521505 18.1784122,41.4153678 C18.1784122,41.6206647 18.1982274,63.2162577 18.1982274,63.2162577 C18.1982274,68.6194672 30.3573497,66.3837838 30.3573497,54.5143374 L30.3573497,49.6011716 L30.3573497,49.600761 L30.3573497,40.0916133 L30.3573497,37.9591942 L30.360033,22.5036213 C30.360033,20.7705047 31.7130419,19.3465653 33.0596521,19.2276984 L33.0596521,19.2279037 C33.1114607,19.2235925 33.1628564,19.2153806 33.2152842,19.2153806 C34.6198953,19.2153806 35.9611389,20.851597 35.9726978,22.4633831 L35.9716657,31.9947029 L35.9726978,31.9947029 L35.9726978,32.0004513 C35.9726978,34.5547555 38.0739381,36.6446781 40.6420748,36.6446781 L43.4622366,36.6446781 C46.0305798,36.6446781 48.1318201,34.5547555 48.1318201,32.0004513 L48.1318201,14.370784 L48.1318201,11.3406016 L48.1318201,10.0767938 C48.1318201,7.797998 49.2231028,6.48430305 50.8219444,6.48430305 C52.4544306,6.48430305 53.7919588,8.40239212 53.8367495,10.1853958 C53.8381944,11.5514415 53.8462443,17.1808882 53.8462443,17.1808882 C53.8462443,19.7544903 56.0816503,19.9606084 58.4941549,19.9606084 C60.2486286,19.9606084 62.2516184,19.2482281 63.7344584,17.4426418 C65.020178,15.8770475 66,14.5452864 66,11.0835698 L66,7.56457541 L66,7.09198191 L66,4.69370336 L66,4.65264397 L66,4.6442268 C66,2.09012789 63.8987597,0 61.3306229,0"
                        ></path>
                      </g>
                    </g>
                  </g>
                </g>
              </svg>
            </a>
          </div>
          <button
            aria-label="Open menu"
            class="hamburger"
            @click="toggleMenu()"
          >
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </button>
        </div>
        <div class="btns-wrp">
          <!-- <a
            href="https://adp.fm/"
            class="adp-fm-link desktop ellipsis"
            target="_blank"
            ><span class="blinking-red"></span>Live on ADP.FM: Ginger Root
          </a>
          <a href="https://adp.fm/" class="adp-fm-link mobile" target="_blank"
            ><span class="blinking-red"></span>Live: ADP.FM</a
          > -->
          <a
            href="https://yr.media/yr-media-community/"
            class="get-involved desktop"
            target="_blank"
            >Get Involved</a
          >
          <a
            href="https://yr.media/yr-media-community/"
            class="get-involved mobile"
            target="_blank"
            >Get Involved</a
          >
          <button
            aria-label="Search for..."
            class="icon-search"
            @click="toggleSeach()"
          ></button>
        </div>
      </div>
      <div :class="['search-container', searchContainer ? 'active' : '']">
        <div class="search-input">
          <form action="https://yr.media/search">
            <input type="text" name="s" />
            <button>Go</button>
          </form>
        </div>
        <button
          aria-label="Search for..."
          class="icon-close"
          @click="toggleSeach()"
        />
      </div>
    </header>
    <nav class="main-navigation">
      <ul id="menu-main-menu" class="main-menu">
        <li
          id="menu-item-35699"
          class="
            menu-item
            menu-item-type-taxonomy
            menu-item-object-category
            menu-item-35699
          "
        >
          <a href="https://yr.media/category/news/">News</a>
        </li>
        <li
          id="menu-item-35695"
          class="
            menu-item
            menu-item-type-taxonomy
            menu-item-object-category
            menu-item-35695
          "
        >
          <a href="https://yr.media/category/arts-culture/">Arts + Culture</a>
        </li>
        <li
          id="menu-item-36929"
          class="
            menu-item
            menu-item-type-taxonomy
            menu-item-object-category
            menu-item-36929
          "
        >
          <a href="https://yr.media/category/identity/">Identity</a>
        </li>
        <li
          id="menu-item-35698"
          class="
            menu-item
            menu-item-type-taxonomy
            menu-item-object-category
            menu-item-35698
          "
        >
          <a href="https://yr.media/category/tech/">Tech</a>
        </li>
        <li
          id="menu-item-35697"
          class="
            menu-item
            menu-item-type-taxonomy
            menu-item-object-category
            menu-item-35697
          "
        >
          <a href="https://yr.media/category/health/">Health</a>
        </li>
        <li
          id="menu-item-36719"
          class="
            menu-item
            menu-item-type-custom
            menu-item-object-custom
            menu-item-36719
          "
        >
          <a href="https://yr.media/tag/opinion/">Opinion</a>
        </li>
      </ul>
      <footer>
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

          <ul id="menu-media-categories-menu" class="media-menu">
            <li
              id="menu-item-82546"
              class="
                menu-item
                menu-item-type-custom
                menu-item-object-custom
                menu-item-82546
              "
            >
              <a href="https://behindourmasks.net/">Behind Our Masks</a>
            </li>
            <li
              id="menu-item-38608"
              class="
                menu-item
                menu-item-type-custom
                menu-item-object-custom
                menu-item-38608
              "
            >
              <a target="_blank" rel="noopener" href="https://adp.fm/"
                >ADP.FM Stream</a
              >
            </li>
            <li
              id="menu-item-36510"
              class="
                menu-item
                menu-item-type-custom
                menu-item-object-custom
                menu-item-36510
              "
            >
              <a href="https://yr.media/adult-ish/">Adult ISH Podcast</a>
            </li>
            <li
              id="menu-item-82312"
              class="
                menu-item
                menu-item-type-post_type
                menu-item-object-page menu-item-82312
              "
            >
              <a href="https://yr.media/ryl-studios-type-beat-challenge/"
                >RYL Studios</a
              >
            </li>
          </ul>
        </div>
        <div>
          <ul id="menu-second-header-menu" class="pages-menu">
            <li
              id="menu-item-57009"
              class="
                menu-item
                menu-item-type-post_type
                menu-item-object-page menu-item-57009
              "
            >
              <a href="https://yr.media/about-yr/">About YR Media</a>
            </li>
            <li
              id="menu-item-66508"
              class="
                menu-item
                menu-item-type-post_type
                menu-item-object-page menu-item-66508
              "
            >
              <a href="https://yr.media/yr-classes/">Apply to Classes</a>
            </li>
            <li
              id="menu-item-63928"
              class="
                menu-item
                menu-item-type-taxonomy
                menu-item-object-category
                menu-item-63928
              "
            >
              <a href="https://yr.media/category/diy/">Our DIY Tools</a>
            </li>
            <li
              id="menu-item-57010"
              class="
                menu-item
                menu-item-type-post_type
                menu-item-object-page menu-item-57010
              "
            >
              <a href="https://yr.media/career-opportunities/">Careers at YR</a>
            </li>
          </ul>
        </div>
      </footer>
    </nav>
  </div>
</template>

<script>
import CommonUtils from '../../mixins/CommonUtils'

export default {
  name: 'MenuHeader',
  mixins: [CommonUtils],
  props: {
    menuFixed: {
      type: Boolean,
      required: false,
      default: true,
    },
    offset: {
      type: Number,
      required: false,
      default: 0,
    },
  },
  data() {
    return {
      activeMenu: false,
      searchContainer: false,
      hideNavbar: true,
      lastScrollY: 0,
    }
  },
  computed: {
    logoFixed() {
      return {
        position: 'fixed',
        top: '10px',
        left: '6px',
        margin: '0px',
      }
    },
  },
  mounted() {
    if (!this.menuFixed) {
      window.addEventListener(
        'scroll',
        (event) => this.debouceEvent(event, this.onScroll),
        false
      )
      this.hideNavbar = false
    }
  },
  methods: {
    onScroll() {
      this.hideNavbar = window.scrollY < this.offset + 83
      this.lastScrollY = window.scrollY
      if (this.activeMenu || this.searchContainer) {
        this.activeMenu = window.scrollY < this.offset + 83
        this.searchContainer = window.scrollY < this.offset + 83
      }
    },
    toggleMenu() {
      if (this.searchContainer) {
        this.toggleSeach()
      }
      this.activeMenu = !this.activeMenu
    },
    toggleSeach() {
      if (this.activeMenu) {
        this.toggleMenu()
      }
      this.searchContainer = !this.searchContainer
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import './assets/style.scss';
</style>
