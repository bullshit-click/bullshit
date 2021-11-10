<template>
  <header id="header">
    <router-link v-bind:to="'/'"><img src="./../../assets/images/header/logo-banniere.svg" class="logo"></router-link>
    <nav class="uppercase">
      <div class="navigation" v-if="$mq === 'laptop'">
        <ul role="navigation">
          <li><router-link v-bind:to="'/podcasts'">PODCASTS</router-link></li>
          <li><router-link v-bind:to="'/shows'">SHOWS</router-link></li>
          <li><router-link v-bind:to="'/prog'">PROG</router-link></li>
          <li><router-link v-bind:to="'/actions'">REPORTAGES/ACTIONS</router-link></li>
          <li><router-link v-bind:to="'/raptz'">RAPTZ</router-link></li>
        </ul>
        <div class="search"><Search /></div>
      </div>
      <div v-else>
        <div class="header__burger-container">
          <Burger/>
        </div>
        <Sidebar/>

      </div>
    </nav>
  </header>
</template>

<style>

header {
    display: flex;
    align-items: center;
    justify-content:space-between;
    background: url("./../../assets/images/nav-bkg-l.svg");
    background-repeat: repeat-x;
    z-index:200;
    height:10em;
    width:100%;
    background-position:0 0;
    background-size: auto 10em;
    position:fixed;
    transition: transform 0.25s ease-in-out;
    }

.navigation {
  display:flex;
  align-items: center;
}

  .search {
    margin-left:1.5em;
  }
  
  .header-unpin{
    transform: translateY(-10.5em);
  }

  .header-pin{
    transform: translateY(0);
  }

  .logo {
    padding: 0 2em 0 4em;
    max-height: 7.2em;
  }

  .header__burger-container {
    margin-right:10vw;
  }

  nav {
    font-family: var(--typo-title);
    color: white;
  }

  nav ul li {
    display: inline-block;
    list-style-type: none;
    font-size:1.6em;
    letter-spacing: 0.03em;
    margin:0 0.1em;
  }

  nav ul li a {
    display: block;
    padding: 1em 0.5em;
    text-decoration: none;
    text-transform: uppercase;
    letter-spacing: .04em;
    margin: 0 1rem;
  }

  li a {
    position: relative;
    color: white;
    transition: all .3s ease-out;
      -webkit-transition: all .4s ease-out;
      -moz-transition: all .3s ease-out;
      -ms-transition: all .3s ease-out;
      -o-transition: all .3s ease-out;
  }

  li a:hover {
    color:  hsl(353, 90%, 55%);
  }

  nav ul li a::after {
      content:'';
      display: block;
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      height: 0;
      width: 100%;
      margin: auto;
      opacity: .5;
      background-image:url("./../../assets/images/header/bkg-MenuItem.svg"); 
      background-repeat: no-repeat;
      background-position: center center;
      background-size: 100%;
      z-index: -1;
      transition-property: opacity, height;
      transition-duration: .4s;
      transition-timing-function: ease-in;
  }

  nav ul li a:hover::after {
      height: 100%;
      opacity: 1;
  }

  @media screen and (min-width: 1270px ) {
  
  header {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    background: url("./../../assets/images/nav-bkg-l.svg");
    background-repeat: repeat-x;
    z-index:200;
    height:10em;
    width:100%;
    background-position:0 0;
    background-size: auto 10em;
    position:fixed;
    transition: transform 0.25s ease-in-out;
  }
}

</style>

<script>
import Sidebar from '@/components/header/Sidebar';
import Burger from '@/components/header/Burger';
import Search from '@/components/header/Search';

var lastKnownScrollY = 0;
var currentScrollY = 0;
var ticking = false;
var idOfHeader = 'header';
var eleHeader = null;
const classes = {
  pinned: 'header-pin',
  unpinned: 'header-unpin'
};

function onScroll () {
  currentScrollY = window.pageYOffset;
  requestTick();
}

function requestTick () {
  if (!ticking) {
    requestAnimationFrame(update);
  }
  ticking = true;
}

function update () {
  if (currentScrollY < lastKnownScrollY) {
    pin();
  } else if (currentScrollY > lastKnownScrollY && currentScrollY > 320) {
    unpin();
  }
  lastKnownScrollY = currentScrollY;
  ticking = false;
}

function pin () {
  if (eleHeader.classList.contains(classes.unpinned)) {
    eleHeader.classList.remove(classes.unpinned);
    eleHeader.classList.add(classes.pinned);
  }
}

function unpin () {
  if (eleHeader.classList.contains(classes.pinned) || !eleHeader.classList.contains(classes.unpinned)) {
    eleHeader.classList.remove(classes.pinned);
    eleHeader.classList.add(classes.unpinned);
  }
}

window.onload = function () {
  eleHeader = document.getElementById(idOfHeader);
  document.addEventListener('scroll', onScroll, false);
};

export default {
  name: 'Header',
  data() {
    return {
      queryParam : 'test query param'
    }
  },
  components:{
    Burger,
    Sidebar,
    Search
  }
};

</script>
