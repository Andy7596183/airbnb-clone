<template>
  <div class="nav-wrapper">
    <!-- mobile menu -->
    <ul class="mobile-nav-menu" :class="{ 'is-opened': menuIsShow }">
      <li>
        <router-link to="/">首頁</router-link>
      </li>
      <hr class="separation-line">
      <li>
        <router-link to="/about">成為房東</router-link>
      </li>
      <li>
        <router-link to="/help">協助</router-link>
      </li>
      <li>
        <router-link to="/register">註冊</router-link>
      </li>
      <li>
        <router-link to="/login">登入</router-link>
      </li>
    </ul>

    <nav class="navbar">
      <div class="nav-brand">
        <router-link to="/">首頁</router-link>
      </div>
      <span class="nav-dropdown-btn" @click="menuIsShow = !menuIsShow">
        <i class="fas fa-chevron-down"></i>
      </span>
      <!-- desktop menu -->
      <ul class="desktop-nav-menu">
        <li>
          <router-link to="/about">成為房東</router-link>
        </li>
        <li>
          <router-link to="/help">協助</router-link>
        </li>
        <li>
          <router-link to="/register">註冊</router-link>
        </li>
        <li>
          <router-link to="/login">登入</router-link>
        </li>
      </ul>
      <!-- <button @click="login">Login</button> -->
    </nav>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      menuIsShow: false
    };
  }
};
</script>


<style lang="scss" scoped>
.navbar {
  position: absolute;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  padding: 20px;
  background-color: transparent;
  z-index: 1000;

  .nav-dropdown-btn {
    margin-left: 10px;
    padding: 10px;
    color: gray;
    display: none;
    cursor: pointer;
    transform: rotate(0deg);
    transition: transform 0.2s linear;
  }

  .nav-brand {
    font-size: 2rem;

    a {
      display: flex;
      align-items: center;
      height: 50px;
      color: #fff;
      transition: color 0.2s linear;
    }
  }

  .desktop-nav-menu {
    margin-left: auto;
    display: flex;
    font-size: 1.2rem;

    li {
      margin: 0 10px;
      position: relative;

      a {
        display: flex;
        align-items: center;
        height: 50px;
        color: #fff;
      }

      &::after {
        content: "";
        position: absolute;
        left: 0;
        right: 0;
        bottom: -10px;
        height: 2px;
        background-color: #fff;
        display: none;
      }

      &:hover::after {
        display: block;
      }
    }
  }
}

.mobile-nav-menu {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 100px 20px 0;
  background-color: #fff;
  z-index: 500;
  display: none;
  flex-direction: column;
  font-size: 1.4rem;
  transform: translateY(-100%);
  transition: transform 0.2s linear;

  &.is-opened {
    transform: translateY(0);
  }

  // affect the next element
  &.is-opened + .navbar .nav-brand a {
    color: palevioletred;
  }

  &.is-opened + .navbar .nav-dropdown-btn {
    transform: rotateZ(180deg);
  }

  .separation-line {
    width: 100%;
    opacity: 0;
    transition: opacity 0.2s linear;
  }

  &.is-opened .separation-line {
    opacity: 1;
  }

  li {
    opacity: 0;
    transition: opacity 0s;

    a {
      display: flex;
      height: 60px;
      align-items: center;
    }
  }

  &.is-opened li {
    opacity: 1;
    transition: opacity 0.1s 0.2s linear;
  }
}

@media only screen and (max-width: 1000px) {
  .desktop-nav-menu {
    display: none !important;
  }

  .mobile-nav-menu {
    display: flex !important;
  }

  .nav-dropdown-btn {
    display: block !important;
  }
}
</style>
