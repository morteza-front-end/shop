<template>
  <div>
    <div id="modal__gallery" class="modal" v-show="showedmodal">
      <div class="modal__content">
        <span class="modal__close" @click="closeModal">&times;</span>
        <div class="modal__body" tabindex="0" @focusout="closeModal">
          <img :src="showModalimg" class="show__gallery" />
        </div>
      </div>
    </div>
    <main class="main">
      <div class="container">
        <ul class="breadcrumb">
          <li class="breadcrumb__item breadcrumb__item--hide">
            <a href="" class="breadcrumb__link"
              ><span class="breadcrumb__span">صفحه اصلی</span></a
            >
          </li>
          <li class="breadcrumb__item">
            <a href="" class="breadcrumb__link"
              ><span class="breadcrumb__span">فهرست محصولات</span></a
            >
          </li>
          <li class="breadcrumb__item">
            <a href="" class="breadcrumb__link"
              ><span class="breadcrumb__span">محصول شماره یک</span></a
            >
          </li>
        </ul>
        <div class="product">
          <div class="product__header">
            <div class="product__expiration">
              <div class="count-down__timer" id="count-dowm__timer">
                {{ difrent }}
              </div>
            </div>
          </div>
          <div class="product__row">
            <div class="prodcut__gallery">
              <div class="gallery">
                <div class="gallery__slideshow">
                  <span class="gallery__count">
                    <span class="gallery__number1">{{ slideIndex + 1 }}</span>
                    <span class="gallery__number2">{{ slideleng }}</span>
                  </span>
                  <div class="gallery__slides">
                    <div class="gallery__slide">
                      <img
                        class="gallery__img"
                        :style="
                          slideIndex === index
                            ? 'display:block;'
                            : 'display:none;'
                        "
                        :src="slide.img"
                        alt=""
                        v-for="(slide, index) in sliderProduct"
                        :key="index"
                        @click="showingModal(slide.img)"
                      />
                    </div>
                  </div>
                  <a @click.prevent="move(-1)" class="gallery__prev"
                    >&#10094;</a
                  >
                  <a @click.prevent="move(1)" class="gallery__next">&#10095;</a>
                </div>
                <div class="gallery__content">
                  <div class="gallery__items">
                    <div
                      class="gallery__item"
                      :class="{
                        'gallery__item--is-acitve': slideIndex === index,
                      }"
                      v-for="(item, index) in sliderProduct"
                      :key="`item-${index}`"
                    >
                      <img
                        :src="item.img"
                        @click="currentSlide(index)"
                        class="gallery__item-img"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="product__left">
              <div class="product__category">دسته وب</div>
              <div class="product__info">
                <h1 class="product__title">محصول شماره یک یک شماره</h1>

                <div class="rating">
                  <div class="rating__star">
                    <span
                      class="rating__rate"
                      :data-title="rate.title"
                      v-for="rate in rating"
                      :key="rate.title"
                      @click="rateWidth = rate.width"
                      @mouseover="handelrateStars"
                    ></span>
                  </div>
                  <div class="rating__fstar" :style="`width:${rateWidth}%;`">
                    <span class="rating__frate"></span>
                    <span class="rating__frate"></span>
                    <span class="rating__frate"></span>
                    <span class="rating__frate"></span>
                    <span class="rating__frate"></span>
                  </div>
                </div>
                <div class="rating-star">
                  4.5
                  <span class="rating__num">(65)</span>
                </div>
              </div>
              <div class="controls">
                <Multiselect
                  :options="colorOption"
                  v-model="selectedColor"
                  placeholder="گزینه خود را وارد کنید..."
                />
                <Multiselect
                  :options="counteryOption"
                  v-model="selectedCountery"
                  placeholder="کشور سازنده را انتخاب کنید..."
                />
                <Multiselect
                  :options="langOptions"
                  v-model="selectedlang"
                  label="name"
                  :multiple="true"
                  :close-on-select="false"
                  :clear-on-select="false"
                  placeholder="زبان مورد علاقه خود را انتخاب کنید!"
                />
              </div>
            </div>
          </div>
        </div>

        <SwiperSlider>
          <template v-slot:title> محصولات مرتبط </template>
          <a
            href="product.html"
            class="swiper-slide"
            v-for="item in 4"
            :key="item"
          >
            <div class="slider__box">
              <div class="slider__image">
                <img
                  :src="require(`../assets/img/slider/${item}.jpg`)"
                  alt=""
                  class="slider__img"
                />
              </div>
              <div class="slider__title2">گوشی موبایل سامسونگ مدل نوت 20</div>
              <div class="slider__price">
                <span class="slider__compare-price">12,200,000</span>
                <span class="slider__total-price">12,400,000 تومان</span>
              </div>
              <span class="slider__discount">%6</span>
            </div>
          </a>
        </SwiperSlider>

        <div class="product-details">
          <div class="tab">
            <div class="tab__items">
              <span
                class="tab__item tab__item--compare"
                :class="{ 'tab__item--is-active': isActiveTab === 'compare' }"
                @click="isActiveTab = 'compare'"
                >نقد و برسی</span
              >
              <span
                class="tab__item tab__item--featrues"
                :class="{ 'tab__item--is-active': isActiveTab === 'featrues' }"
                @click="isActiveTab = 'featrues'"
                >ویژیگی ها</span
              >
              <span
                class="tab__item tab__item--comments"
                :class="{ 'tab__item--is-active': isActiveTab === 'comments' }"
                @click="isActiveTab = 'comments'"
                >نظرات</span
              >
            </div>
            <div class="tab__sections">
              <Compre
                :style="
                  isActiveTab === 'compare' ? 'display:block;' : 'display:none;'
                "
              />
              <Featrues
                :style="
                  isActiveTab === 'featrues'
                    ? 'display:block;'
                    : 'display:none;'
                "
              />
              <Comments
                :style="
                  isActiveTab === 'comments'
                    ? 'display:block;'
                    : 'display:none;'
                "
              />
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import moment from "moment";
import "../assets/css/modal.css";
import Multiselect from "vue-multiselect";
import "vue-multiselect/dist/vue-multiselect.min.css";
import SwiperSlider from "../components/SwiperSlider";
import Compre from "../components/Tabs/Compre.vue";
import Featrues from "../components/Tabs/Featrues.vue";
import Comments from "../components/Tabs/Comments.vue";
export default {
  name: "Product",
  components: {
    Multiselect,
    SwiperSlider,
    Compre,
    Featrues,
    Comments,
  },
  metaInfo: {
    title: "نمایش  محصول",
  },
  data: () => ({
    dateCountdown: moment("2021-11-07 00:00:00"),
    isActiveTab: "compare",
    difrent: null,
    slides: [
      { img: require("../assets/img/slideshow/1.png") },
      { img: require("../assets/img/slideshow/2.png") },
      { img: require("../assets/img/slideshow/3.png") },
      { img: require("../assets/img/slideshow/4.png") },
    ],
    sliderProduct: [
      { img: require(`../assets/img/gallery/1.jpg`) },
      { img: require(`../assets/img/gallery/2.jpg`) },
      { img: require(`../assets/img/gallery/3.jpg`) },
      { img: require(`../assets/img/gallery/4.jpg`) },
      { img: require(`../assets/img/gallery/4.jpg`) },
      { img: require(`../assets/img/gallery/3.jpg`) },
      { img: require(`../assets/img/gallery/2.jpg`) },
      { img: require(`../assets/img/gallery/1.jpg`) },
    ],
    rating: [
      { width: 100, title: "عالی" },
      { width: 80, title: "خیلی خوب" },
      { width: 60, title: "خوب" },
      { width: 40, title: "متوسط" },
      { width: 20, title: "بد" },
    ],
    rateWidth: 0,
    slideIndex: 0,
    showedmodal: false,
    showModalimg: null,
    selectedColor: "",
    colorOption: ["قرمز", "آبی", "زرد"],
    counteryOption: ["ایران", "کره جنوبی", "چین", "فرانسه", "آمریکا"],
    selectedCountery: [],
    langOptions: [
      { name: "Vue.js", language: "JavaScript" },
      { name: "Rails", language: "Ruby" },
      { name: "Sinatra", language: "Ruby" },
      { name: "Laravel", language: "PHP" },
      { name: "Phoenix", language: "Elixir" },
    ],
    selectedlang: [],
  }),
  methods: {
    move(n) {
      if (this.sliderProduct.length <= this.slideIndex + n) {
        this.slideShowIndex = 0;
      } else if (this.slideIndex + n < 0) {
        this.slideIndex = this.sliderProduct.length - 1;
      } else {
        this.slideIndex += n;
      }
    },

    currentSlide(index) {
      this.slideIndex = index;
    },
    showingModal(image) {
      this.showedmodal = true;
      this.showModalimg = image;
      document.body.style.overflow = "hidden";
    },
    closeModal() {
      this.showedmodal = false;
      document.body.style.overflow = "unset";
    },
    handelrateStars() {
      this.rateWidth = 0;
    },
  },
  created() {
    setInterval(() => {
      let diffTime = this.dateCountdown.diff(moment());
      let durTime = moment.duration(diffTime);
      this.difrent = `${Math.floor(
        durTime.asDays()
      )}:${durTime.hours()}:${durTime.minutes()}:${durTime.seconds()}`;
    }, 1000);
    this.slideleng = this.sliderProduct.length;
  },
  destroyed() {
    clearInterval();
  },
};
</script>

<style>
</style>