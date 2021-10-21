<template>
  <main class="main">
    <div class="container">
      <div class="page">
        <div class="page__sidebar">
          <div class="box" v-show="selectItemes.length > 0">
            <div class="box-filters">
              <div class="box-filters__header">
                <span class="box-filters__title">فیلتر های اعمال شده</span>
                <a
                  style="cursor: pointer"
                  class="box-filters__clear"
                  @click.prevent="removeAllFilters"
                  >حذف همه</a
                >
              </div>
              <ul class="box-filters__ul">
                <li
                  class="box-filters__li"
                  v-for="filter in selectItemes"
                  :key="filter"
                >
                  <button
                    class="box-filters__button"
                    @click="removeFilter(filter)"
                  ></button>
                  <span class="box-filters__name">{{ filter }}</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="box">
            <div class="box__row" @click="isShowBoxBrand = !isShowBoxBrand">
              <div
                class="box__header"
                :class="isShowBoxBrand ? ' ' : 'box--togglable'"
                ref="showbox"
              >
                برند ها
              </div>
              <div
                class="box__filter"
                :style="isShowBoxBrand ? ' ' : 'display:none;'"
              >
                <div class="box__content-container">
                  <div class="box__content">
                    <ul class="box__ul">
                      <li class="box__li">
                        <label
                          class="ui-checkbox"
                          data-fa="سامسونگ"
                          data-en="Sumsung"
                          data-serach="Sumsung سامسونگ"
                        >
                          <input
                            type="checkbox"
                            v-model="selectItemes"
                            value="سامسونگ"
                            class="ui-checkbox__input"
                          />
                          <span class="ui-checkbox__mark"></span>
                          سامسونگ
                        </label>
                      </li>
                      <li class="box__li">
                        <label
                          class="ui-checkbox"
                          data-fa="سونی"
                          data-en="sony"
                          data-serach="sony سونی"
                        >
                          <input
                            type="checkbox"
                            v-model="selectItemes"
                            value="سونی"
                            class="ui-checkbox__input"
                          />
                          <span class="ui-checkbox__mark"></span>
                          سونی
                        </label>
                      </li>
                      <li class="box__li">
                        <label
                          class="ui-checkbox"
                          data-fa="اپل"
                          data-en="apple"
                          data-serach="apple اپل"
                        >
                          <input
                            type="checkbox"
                            v-model="selectItemes"
                            value="اپل"
                            class="ui-checkbox__input"
                          />
                          <span class="ui-checkbox__mark"></span>
                          اپل
                        </label>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="box">
            <div class="box__row" @click="isShowBoxColor = !isShowBoxColor">
              <div
                class="box__header"
                :class="isShowBoxColor ? ' ' : 'box--togglable'"
              >
                رنگ ها
              </div>
              <div
                class="box__filter"
                :style="isShowBoxColor ? ' ' : 'display:none;'"
              >
                <div class="box__content-container">
                  <div class="box__content">
                    <ul class="box__ul">
                      <li class="box__li">
                        <label
                          class="ui-checkbox"
                          data-fa="مشکی"
                          data-serach="balck مشکی"
                        >
                          <input
                            type="checkbox"
                            class="ui-checkbox__input"
                            v-model="selectItemes"
                            value="مشکی"
                          />
                          <span class="ui-checkbox__mark"></span>
                          مشکی
                          <span
                            class="filter__color"
                            style="background: rgb(0, 0, 0)"
                          ></span>
                        </label>
                      </li>
                      <li class="box__li">
                        <label
                          class="ui-checkbox"
                          data-fa="آبی"
                          data-serach="blue آبی"
                        >
                          <input
                            type="checkbox"
                            class="ui-checkbox__input"
                            v-model="selectItemes"
                            value="آبی"
                          />
                          <span class="ui-checkbox__mark"></span>
                          آبی
                          <span
                            class="filter__color"
                            style="background: rgb(0, 0, 255)"
                          ></span>
                        </label>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="box box--switcher">
            <label class="ui-switcher">
              <input type="checkbox" class="ui-switcher__input" />
              <span class="ui-switcher__slider">
                <span class="ui-switcher__toggle"></span>
              </span>
              فقط کالای های موجود
            </label>
          </div>
        </div>
        <div class="page__content">
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
          <div class="products">
            <router-link
             :to="{name:'Product',params:{id:index}}"
              class="products__item"
              v-for="(item,index) in 6"
              :key="item"
            >
              <div class="card">
                <div class="card__image">
                  <img
                    :src="require(`../assets/img/slider/${item}.jpg`)"
                    alt=""
                    class="card__img"
                  />
                </div>
                <div class="card__title">گوشی موبایل سامسونگ مدل نوت 20</div>
                <div class="card__price">
                  <span class="card__compare-price">12,200,000</span>
                  <span class="card__total-price">12,400,000 تومان</span>
                </div>
                <span class="card__discount">%6</span>
              </div>
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Category",
  data: () => ({
    isShowBoxBrand: false,
    isShowBoxColor: false,
    selectItemes: [],
    isShowfilterBox: false,
  }),
  methods: {
    removeAllFilters() {
      this.selectItemes = [];
    },
    removeFilter(filter) {
      this.selectItemes = this.selectItemes.filter((item) => item !== filter);
    },
    // showFilterBox() {
    //   if (this.selectItemes.length > 0) {
    //     this.isShowfilterBox = true;
    //   } else {
    //     this.isShowfilterBox = false;
    //   }
    // },
  },
  mounted() {},
  metaInfo: {
    title: "دسته بندی محصولات",
  },
};
</script>

<style>
</style>