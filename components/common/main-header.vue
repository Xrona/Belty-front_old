<template>
  <div class="row">
    <div class="col-12">
      <div
        class="flex items-center justify-between xl:justify-start xl:gap-5 relative py-4"
      >
        <button
          v-click-outside="hideMenu"
          class="burger-button xl:hidden"
          :class="{ active: menu }"
          @click="toggleMenu"
        >
          <span></span>
        </button>
        <transition name="slide">
          <template v-if="menu">
            <div
              class="absolute z-10 w-full p-3 bg-white flex flex-col gap-2 top-14 base-shadow rounded-2 xl:hidden"
            >
              <template v-for="item in $options.menuList">
                <nuxt-link :key="item.name" class="menu-item" :to="item.link">
                  {{ item.name }}
                </nuxt-link>
              </template>
            </div>
          </template>
        </transition>
        <div class="flex gap-4">
          <nuxt-link to="/" class="text-h1 text-black-60">Belty</nuxt-link>
          <button
            class="bg-blue-60 text-white h-9 w-9 rounded-2"
            @click="goToCart"
          >
            <svg-icon name="logo-cart" width="28" height="27" />
          </button>
        </div>
        <div class="hidden xl:flex gap-3 flex-grow justify-end">
          <template v-for="item in $options.menuList">
            <nuxt-link
              :key="`md-${item.name}`"
              :to="item.link"
              class="menu-item"
            >
              {{ item.name }}
            </nuxt-link>
          </template>
        </div>
        <div class="hidden xl:flex gap-2 items-center">
          <profile-avatar />
          <div class="flex flex-col gap-1">
            <span class="text-black-60 text-h3 font-jura">Иванов Иван</span>
            <nuxt-link to="/logout" class="link-button h-[29px]"
              >Выйти</nuxt-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ClickOutside from 'vue-click-outside'
import ProfileAvatar from '@/components/common/profile-avatar'
export default {
  name: 'MainHeader',
  components: { ProfileAvatar },
  directives: {
    ClickOutside,
  },

  data() {
    return {
      menu: false,
    }
  },

  methods: {
    toggleMenu() {
      this.menu = !this.menu
    },

    hideMenu() {
      this.menu = false
    },

    goToCart() {
      this.$router.push('/profile/cart')
    },
  },

  menuList: [
    {
      name: 'Каталог',
      link: '/catalog',
    },
    {
      name: 'Акции',
      link: '/',
    },
    {
      name: 'О нас',
      link: '/',
    },
    {
      name: 'Оформление заказа',
      link: '/',
    },
    {
      name: 'Оплата и доставка',
      link: '/',
    },
    {
      name: 'Блог',
      link: '/',
    },
    {
      name: 'Контакты',
      link: '/',
    },
  ],
}
</script>
