<template>
  <div class="navbar" id="navbar">
      <a href="/" class="navbar-logo">
          <img src="../assets/logo.png" alt="Logo Kajaki Na Kaszubach - Kajax" class="navbar-logo__img">
          <h1 class="navbar-logo__title">KAJAX - Kajaki na kaszubach</h1>
      </a> 
      <input id="menu-btn" class="ham" type="checkbox" v-on:click="toggleHamburgerMenu()"/>
      <label class="ham-menu-icon" for="menu-btn"></label>
      <nav class="nav">
          <ul class="menu">
              <li class="menu__list-item"><a href="/#road">Spływy</a> </li>
              <li class="menu__list-item"><a href="/#wypozyczalnia">Wypożyczalnia</a> </li>
              <li class="menu__list-item"><nuxt-link to="/hut">Domki</nuxt-link> </li>
              <li class="menu__list-item"><a href="/#kontakt">Kontakt</a> </li>
          </ul>
      </nav>
  </div>
</template>

<script>
export default {
    methods:{
        changeMenuOnFullHeightScroll(){
            const navbar = document.querySelector('#navbar')
            let lastKnownScrollPosition = 0
            let windowHeight = window.innerHeight
            console.log(navbar.offsetHeight);
            document.addEventListener('scroll',()=>{
                lastKnownScrollPosition = this.watchScrollPosition()
                if(lastKnownScrollPosition >= (windowHeight - navbar.offsetHeight) ){
                    navbar.classList.add('navbar--full')
                }
                else{
                    navbar.classList.remove('navbar--full')
                }
            })
        },
        watchScrollPosition(){
            return window.scrollY
        },
        toggleHamburgerMenu(){
            const navbar = document.querySelector('.nav')
            const ham = document.querySelector('.ham')
            navbar.classList.toggle("showNav");
        },
    },
    beforeMount(){
        this.changeMenuOnFullHeightScroll()
    }
}
</script>

<style>
    .navbar{
        position: fixed;
        left:50%;
        z-index: 99999;
        display: flex;
        flex-wrap: wrap;
        width:100%;
        max-width: 1300px;
        height: 80px;
        background-color: rgba(0,0,0,0);
        font-family: 'Montserrat';
        font-size: 16px;
        transform: translateX(-50%);
    }
    .navbar--full{
        background-color: #FFF;
        max-width: 100%;
        padding: 0 2rem;
        box-shadow: 0 0 4px 2px rgb(192, 192, 192);
        color:#000;
    }
    .navbar--full .menu{
        color:#000;
    }
    .navbar-logo{
        display: flex;
        align-items: center;
        min-width: 360px;
        width: 40%;
        background-color: #FFF;
        transition: 1s ease all;
    }
    .navbar-logo__img{
        width: 53.1px;
        height: 50px;
    }
    .navbar-logo__title{
        margin-left: 1.5rem;
        font-size: 1.1rem;
        font-weight: bold;
    }
    .nav{
        display: flex;
        justify-content: flex-end;
        align-items: center;
        width: 60%;
    }
    .menu{
        display: flex;
        list-style-type: none;
        font-size: 1rem;
        color:#FFF;
    }
    .menu__list-item{
        text-transform: uppercase;
        margin-left: 1rem;
    }
    .ham{
        display: none;
    }
    @media screen and (max-width:1000px) {
    .navbar{
        justify-content: space-between;
        align-items: center;
        padding: 0 1rem;
        background-color: #FFF;
    }
    .navbar-logo{
        color: #000;
    }
    .navbar--full .navbar-logo{
        color:#000;
    }
    .nav{
        position: fixed;
        top: 0;
        left: 0;
        background: #005492;
        width: 100vw;
        height: 50vh;
        box-shadow: 0 0 4px 2px #007ad1;
        overflow: hidden;
        color: white;
        /* hide the menu above the screen by default */
        transform: translateY(-100%);
        /* transition adds a little animation when sliding in and out the menu */
        transition: transform 0.2s ease;
    }
    .ham {
        position: relative;
        display: block;
        visibility: hidden;
        z-index: 1000;
        top: 20px;
        right: 20px;
        width: 30px;
        height: 30px;
        border: none;
        cursor: pointer;
        background-color: transparent;
        /* show the menu image */
        background-size: 100%;
    }
    .ham-menu-icon,
    .ham-menu-icon::before,
    .ham-menu-icon::after{
        position: absolute;
        width: 30px;
        height: 5px;
        border-radius: 5px;
        background-color: #000;
        transition: 0.6s;
    }
    .ham-menu-icon{
        cursor: pointer;
        top:50%;
        right: 1rem;
        z-index: 1000;
    }
    .ham-menu-icon::before{
        content: '';
        transform: translateY(-10px);
    }
    .ham-menu-icon::after{
        content: '';
        transform: translateY(10px);
    }
    .ham:checked + .ham-menu-icon{
        width:0px;
        right: 3rem;
    }
    .ham:checked + .ham-menu-icon:before{
        transform: rotate(45deg) translate(0px);
    }
    .ham:checked + .ham-menu-icon:after{
        transform: rotate(-45deg) translate(0px);
    }
    .showNav {
        /* show the menu */
        transform: translateY(0);
    }
    .navbar--full .menu,.menu{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        height: 100%;
        padding: 5rem 0;
        color:#FFF;
    }
    .menu__list-item{
        height: 60px;
        margin: 0 1rem;
    }
    }
    
    @media screen and (max-width:500px) {
    .navbar-logo{
        min-width: auto;
        width: auto;
    }
    .navbar-logo__title{
        font-size: 1rem;
        margin-left: 1rem;
    }
    .navbar-logo__img{
        width: 45px;
        height: 40px;
    }
    }
</style>