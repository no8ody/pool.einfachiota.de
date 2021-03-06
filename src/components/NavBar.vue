<template>
  <nav v-bind:class="{ open: navStateOpen }" class="main-nav">
    <router-link to="/" class="nav-item nav-item--logo" exact-active-class="active">
      Pool
    </router-link>

    <div v-bind:class="{ open: navStateOpen }" class="menu-btn-container" @click="toggleNav">
      <div class="menu-btn">
        <span class="top"></span>
        <span class="center"></span>
        <span class="bottom"></span>
      </div>
    </div>

    <div v-bind:class="{ open: navStateOpen }" class="nav-menu">
      <router-link v-on:click.native="navStateOpen = false" to="/" class="nav-item" active-class="active">
        <span >Home</span>
      </router-link>
      <router-link v-on:click.native="navStateOpen = false" to="/register" class="nav-item" active-class="active">
      <span ><i18n path="nav_register"></i18n></span>
      </router-link>

      <div v-on:click="switchLanguage()" class="lang">
          <!-- <span>Switch Language </span> -->
          <img v-if="this.$i18n.locale != 'de'"
            alt="lang" 
            class="logo" 
            src="../plugins/ger-flag.png" 
            contain   
            height="20rm"
          >
          <img v-else
            alt="lang" 
            class="logo" 
            src="../plugins/us-flag.png" 
            contain   
            height="20rm"
          >
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      navStateOpen: false
    };
  },
  methods: {
    toggleNav() {
      this.navStateOpen = !this.navStateOpen;
    },
    switchLanguage(){
      if(this.$i18n.locale == 'de'){
        this.$i18n.locale = 'en'
      } else {
        this.$i18n.locale = 'de'
      }
    }
  },
      mounted() {
      console.log("mounted");
      let userLang = navigator.language || navigator.userLanguage; 
      if(userLang.slice(0,2) == 'de'){
        this.$i18n.locale = 'de'
      }
    }
};
</script>

<style lang="scss">
// ------------------------------------------
//  N A V I G A T I O N
// ------------------------------------------

.main-nav {
  position: fixed;
  top: 50px;
  left: 0;
  z-index: 10;
  height: 70px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--dark);
  border-bottom: 5px solid var(--primary);
  transition: all 200ms ease-in-out;
  .lang {
    margin-right: 40px;
    margin-left: 20px;
  }
  .menu-btn {
    display: none;
  }
  .nav-menu {
    height: 100%;
    display: flex;
    align-items: center;
  }
  .nav-item {
    position: relative;
    overflow: hidden;
    height: 100%;
    padding: 0 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: var(--dark);
    font-family: "Roboto Slab";
    font-weight: bold;
    text-decoration: none;
    opacity: 0.75;
    transition: all 200ms ease-in-out;
    &--logo {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0 20px;
      opacity: 1;
      img.logo {
        width: auto;
        height: 45px;
        transition: all 200ms ease-in-out;
      }
    }
    &:before {
      content: "";
      position: absolute;
      top: -5px;
      height: 10px;
      width: 0;
      border-radius: var(--border-radius);
      transition: all 200ms ease-in-out;
    }
    &:hover,
    &.active {
      opacity: 1;
      background-color: var(--black_5);
      color: var(--primary);
      &:before {
        content: "";
        position: absolute;
        top: -5px;
        bottom: -5px;
        height: 10px;
        width: 50px;
        border-radius: var(--border-radius);
        background-color: var(--primary);
      }
    }
    &:hover {
      cursor: pointer;
      &:before {
        width: 10px;
      }
    }
  }
}

// ------------------------------------------
//  M O B I L E
// ------------------------------------------

@media only screen and (max-width: 1100px) {
  .main-nav {
    top: 50px;
    .nav-menu {
      .nav-item {
        padding: 0 40px;
      }
    }
  }
}


@media only screen and (max-width: 992px) {
  .main-nav {
    top: 50px;
    .lang {
      margin: 20px auto;
    }
    &.open {
      background-color: var(--dark);
      &.normal {
        background-color: var(--dark);
      }
    }
    .menu-btn-container {
      height: 70px;
      width: 70px;
      display: flex;
      justify-content: center;
      align-items: center;
      transition: all 300ms ease-in-out;
      .menu-btn {
        position: relative;
        height: 29px;
        width: 29px;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: all 300ms ease-in-out;
        span {
          position: absolute;
          height: 3px;
          width: 100%;
          background-color: var(--light);
          border-radius: var(--border-radius-sm);
          transition: all 300ms ease-in-out;
        }
        .top {
          top: 5px;
        }
        .bottom {
          bottom: 5px;
        }
      }
      &.open {
        background-color: var(--dark);
        .menu-btn {
          transform: rotate(180deg);
        }
        .center {
          width: 3px;
        }
        .top {
          transform: rotate(45deg);
          top: 13px;
        }
        .bottom {
          transform: rotate(-45deg);
          bottom: 13px;
        }
      }
      &:hover {
        cursor: pointer;
        background-color: var(--white_10);
        .center {
          width: 15px;
        }
        .top,
        .bottom {
          width: 25px;
        }
      }
      &.open:hover {
        .center {
          width: 3px;
        }
      }
      &.normal {
        span {
          background-color: var(--dark);
        }
        &:hover {
          background-color: var(--black_10);
        }
      }
    }
    .nav-menu {
      display: none;
      .nav-item {
        height: 100px;
        border-bottom: var(--border-sm_light);
        &:first-child {
          border-top: var(--border-sm_light);
        }
        &:before {
          left: -5px;
          bottom: auto;
          width: 10px;
          height: 50px;
          top: 25px;
        }
      }
      &.open {
        position: fixed;
        top: 70px;
        left: 0;
        width: 100%;
        height: calc(100vh - 70px);
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: stretch;
        background-color: var(--dark);
      }
      &.normal {
        background-color: var(--dark);
        .nav-item {
          border-bottom: var(--border-sm_dark);
          &:first-child {
            border-top: var(--border-sm_dark);
          }
        }
      }
    }
  }
}


@media only screen and (max-width: 480px) {
  .main-nav {
    top: 80px;
    .nav-menu {
      .nav-item {
        padding: 0 40px;
      }
    }
  }
}
</style>