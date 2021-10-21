<template>
  <header class="header header--bg">
    <div class="header__shape">
      <div class="header__shape-inner"></div>
    </div>
    <div class="container">
      <div class="navbar">
        <div class="navbar__row">
          <div class="header__logo">
            <router-link
              to="/"
              @click="activeNav = 'home'"
              class="header__logo-img"
            ></router-link>
          </div>
          <div
            class="navbar__items"
            :class="{ 'navbar__items--is-active': showbtnSlidemenu }"
          >
            <ul class="navbar__ul">
              <li class="navbar__item" @click="activeNav = 'home'">
                <router-link
                  to="/"
                  class="navbar__link"
                  :class="{ ' navbar__link--is-active': activeNav === 'home' }"
                  >صفحه اصلی</router-link
                >
              </li>
              <li
                class="navbar__item navbar__item--has-sub"
                @click="activeNav = 'shop'"
              >
                <router-link
                  :to="{ name: 'Category' }"
                  class="navbar__link"
                  :class="{ ' navbar__link--is-active': activeNav === 'shop' }"
                  >فروشگاه</router-link
                >
              </li>
              <li
                class="navbar__item navbar__item--has-sub"
                @click.prevent="activeNav = 'services'"
              >
                <a
                  href=""
                  class="navbar__link"
                  :class="{
                    ' navbar__link--is-active': activeNav === 'services',
                  }"
                  >خدمات</a
                >
                <ul class="navbar__subset">
                  <li class="navbar__item">
                    <a href="" class="navbar__link">زیر منو 1</a>
                  </li>
                  <li class="navbar__item">
                    <a href="" class="navbar__link">زیر منو 2</a>
                  </li>
                  <li class="navbar__item navbar__item--has-sub">
                    <a href="" class="navbar__link">زیر منو 3</a>
                    <ul class="navbar__subset">
                      <li class="navbar__item">
                        <a href="" class="navbar__link">زیر منو 1</a>
                      </li>
                      <li class="navbar__item">
                        <a href="" class="navbar__link">زیر منو 2</a>
                      </li>
                      <li class="navbar__item navbar__item--has-sub">
                        <a href="" class="navbar__link">زیر منو 3</a>
                        <ul class="navbar__subset">
                          <li class="navbar__item">
                            <a href="" class="navbar__link">زیر منو 1</a>
                          </li>
                          <li class="navbar__item">
                            <a href="" class="navbar__link">زیر منو 2</a>
                          </li>
                          <li class="navbar__item">
                            <a href="" class="navbar__link">زیر منو 3</a>
                          </li>
                        </ul>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
              <li class="navbar__item" @click="activeNav = 'about'">
                <router-link
                  :to="{ name: 'About' }"
                  class="navbar__link"
                  :class="{ ' navbar__link--is-active': activeNav === 'about' }"
                  >درباره ما</router-link
                >
              </li>
              <li class="navbar__item" @click.prevent="activeNav = 'contactus'">
                <a
                  href=""
                  class="navbar__link"
                  :class="{
                    ' navbar__link--is-active': activeNav === 'contactus',
                  }"
                  >تماس باما</a
                >
              </li>
            </ul>
          </div>
          <div class="navbar__action">
            <div class="header__basket">
              <router-link
                :to="{ name: 'Card' }"
                class="header__basket-icon"
                @click="showDropDownBasket"
              ></router-link>
              <span class="header__basket-count">0</span>
              <div
                class="header__dropdown"
                :class="{ 'header__dropdown--is-active': isBasketDropDown }"
              >
                <div
                  class="
                    header__dropdown-content header__dropdown-content--overflow
                  "
                >
                  <div
                    class="header__basket-item"
                    v-for="item in 3"
                    :key="item"
                  >
                    <a href="" class="header__basket-link">
                      <img
                        :src="require('../assets/img/big-pic.jpg')"
                        class="header__basket-img"
                      />
                    </a>
                    <div class="header__basket-details">
                      <h5>
                        <a class="header__basket-title" href=""
                          >محصول شماره یک</a
                        >
                      </h5>
                      <div class="header__basket-price">120000 تومان</div>
                      <a href="" class="header__basket-remove">حذف</a>
                    </div>
                  </div>
                  <div class="header__basket-btn">
                    <router-link
                      :to="{ name: 'Login' }"
                      class="btn btn--boxshadow btn--brand w--100"
                      >ثبت و نهایی کردن سفارش</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
            <div class="header__account">
              <span
                class="header__account-icon"
                @click="showDropDownAccount"
              ></span>
              <div
                class="header__dropdown header__dropdown--w200"
                :class="{ 'header__dropdown--is-active': isAccountDropDown }"
              >
                <div class="header__dropdown-content">
                  <router-link
                    :to="{ name: 'Login' }"
                    class="header__account-link"
                    >ورود</router-link
                  >
                  <router-link
                    :to="{ name: 'Register' }"
                    class="header__account-link"
                    >ثبت نام</router-link
                  >
                </div>
              </div>
            </div>
            <div
              class="header__menu"
              @click="showSlideMenu"
              :class="{ 'header__menu--is-active': showbtnSlidemenu }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "BaseHeader",

  data: () => ({
    isBasketDropDown: false,
    isAccountDropDown: false,
    showbtnSlidemenu: false,
    activeNav: "home",
  }),
  components: {},

  methods: {
    showDropDownBasket() {
      this.isAccountDropDown = false;
      this.isBasketDropDown = !this.isBasketDropDown;
    },
    showDropDownAccount() {
      this.isBasketDropDown = false;
      this.isAccountDropDown = !this.isAccountDropDown;
    },
    eventListener(event) {
      if (!event.target.closest(".header__basket,.header__account")) {
        this.isBasketDropDown = false;
        this.isAccountDropDown = false;
      }
      if (!event.target.closest(".header__menu")) {
        this.showbtnSlidemenu = false;
        this.$emit("show-overlay", this.showbtnSlidemenu);
      }
    },
    showSlideMenu() {
      this.showbtnSlidemenu = !this.showbtnSlidemenu;
      this.$emit("show-overlay", this.showbtnSlidemenu);
    },
  },

  mounted() {
    document.addEventListener("click", this.eventListener);
  },

  destroyed() {
    document.removeEventListener("click", this.eventListener);
  },
};
</script>

<style>
</style>