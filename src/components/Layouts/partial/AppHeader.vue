<template>
  <v-app-bar class="header">
    <v-container>
      <div class="header_middle">
        <v-row class="align-center">
          <v-col cols="6" md="3">
            <h1 class="nobletp-logo" data-text="Nobletp">Nobletp</h1>
          </v-col>
          <v-col cols="5" class="d-none d-md-block">
            <div style="position: relative; width: 85%">
              <input
                class="header_middle_input"
                type="search"
                name="NavSearch"
                id="NavSearch"
                placeholder="search the Store"
              />
              <SearchIcon />
            </div>
          </v-col>
          <v-col cols="4">
            <div class="header_middle_right">
              <div class="app_nav_available_text d-none d-md-block">
                <p>available 24/7 at</p>
                <p>(090) 123-456</p>
              </div>
              <div class="header_middle_icons">
                <div class="header_middle_icons_wishlist">
                  <HeartIcon />

                  <span>wishlist</span>
                </div>
                <div class="header_middle_icons_login">
                  <LogInIcon />
                  <span>SignIn</span>
                </div>

                <div class="header_middle_icons_cart" @click="openCart">
                  <CartIcon />
                  <p class="badge">22</p>
                  <span>Cart</span>
                </div>
              </div>
            </div>
          </v-col>
        </v-row>
      </div>
      <div class="header_bottom">
        <v-row class="align-center">
          <v-col cols="12" md="7">
            <ul class="header_bottom_links">
              <li>Theme demo</li>
              <li>Shop</li>
              <li>Product</li>
              <li>new In</li>
              <li>Must Have</li>
            </ul>
          </v-col>
          <v-col cols="12" md="5">
            <div class="header_bottom_right">
              <div class="help">
                <HelpIcon />
                <span>Cart</span>
              </div>
              <div class="lang" id="lang-menu">
                <component :is="selectedLang[0].icon"></component>
                <span
                  >{{ selectedLang[0].lang }}/{{
                    selectedLang[0].currency
                  }}</span
                >
                <v-menu activator="#lang-menu">
                  <v-list v-model:selected="selectedLang">
                    <v-list-item
                      v-for="(lang, index) in langs"
                      :key="index"
                      :value="lang"
                    >
                      <v-list-item-title>
                        <component class="mr-2" :is="lang.icon"></component
                        >{{ lang.lang }} /
                        {{ lang.currency }}
                      </v-list-item-title>
                    </v-list-item>
                  </v-list>
                </v-menu>
                <!-- {{ selectedLang }} -->
              </div>
            </div>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </v-app-bar>
</template>
<script>
import HeartIcon from "@/svg/HeaderIcons/HeartIcon.vue";
import LogInIcon from "@/svg/HeaderIcons/LogInIcon.vue";
import CartIcon from "@/svg/HeaderIcons/CartIcon.vue";
import HelpIcon from "@/svg/HeaderIcons/HelpIcon.vue";
import LangIcon from "@/svg/HeaderIcons/LangIcon.vue";
import DeLangIcon from "@/svg/HeaderIcons/DeLangIcon.vue";
import SearchIcon from "@/svg/HeaderIcons/SearchIcon.vue";
import { markRaw } from "vue";
export default {
  name: " HeaderSection ",

  inject: ["Emitter"],
  components: {
    HeartIcon,
    LogInIcon,
    CartIcon,
    HelpIcon,
    LangIcon,
    DeLangIcon,
    SearchIcon,
  },
  data() {
    return {
      selectedLang: [
        {
          icon: markRaw(LangIcon),
          lang: "EN",
          currency: "USD",
        },
      ],

      langs: [
        {
          icon: markRaw(LangIcon),
          lang: "EN",
          currency: "USD",
        },
        {
          icon: markRaw(DeLangIcon),
          lang: "DE",
          currency: "EUR",
        },
      ],
    };
  },
  methods: {
    openCart() {
      this.Emitter.emit("openCart");
    },
  },
};
</script>
<style lang="scss">
.v-toolbar__content {
  height: fit-content !important;
}

.header {
  padding: 20px 0;
  background: #02218f !important;

  .cart,
  .lang {
    cursor: pointer;
    transition: width 2s;
  }
}

.header_middle {
  &_input {
    width: 85%;
    padding: 10px 12px;
    background: white !important;
    outline: none;
    border-radius: 30px;
  }

  &_input {
    width: 100%;
    padding: 10px 12px;
    background: white !important;
    outline: none;
    border-radius: 30px;
  }

  &_right {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
  }

  &_icons {
    display: flex;

    span {
      color: orange;
    }

    > div:not(:last-child) {
      margin-right: 30px;
    }
  }
  &_icons_cart {
    position: relative;
    .badge {
      background: blue;
      border-radius: 50%;
      text-align: center;
      top: -8px;
      position: absolute;
      right: -11px;
      padding: 0 4px;
    }
  }
}

.header_bottom {
  &_links {
    list-style: none;
    flex-wrap: wrap;

    li {
      display: inline-block;
      color: white;
    }

    > li:not(:last-child) {
      margin-right: 25px;
    }
  }

  &_right {
    display: flex;
    justify-content: end;
    align-items: center;
    color: white;

    div:first-child {
      margin-right: 40px;
    }

    span,
    .v-icon {
      vertical-align: text-bottom;
      margin-left: 5px;
    }
  }
}

.nobletp-logo {
  $h1-background-color: #00203fff; // Dark blue
  $h1-text-color: #ffffff; // White
  $h1-glow-colors: #00c6fb, #00e0ff, #92fe9d; // Shades of blue and green

  $h1-font-size: 3rem;

  font-size: $h1-font-size;
  font-weight: bold;
  color: $h1-text-color;
  text-align: center;
  text-transform: uppercase;
  position: relative;
  overflow: hidden;
  display: inline-block;

  &:before {
    content: attr(data-text);
    position: absolute;
    top: 0;
    left: 0;
    color: $h1-glow-colors;
    mix-blend-mode: screen;
    z-index: -1;
    animation: glowing 3s linear infinite;
    opacity: 0.7; // Adjust the glow opacity as needed
  }
}

@keyframes glowing {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
