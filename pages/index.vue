<template>
  <div class="container">
    <Header />
    <About />
    <Road />
    <Feedback />
    <Equipment />
    <Experience />
    <Hut />
    <Footer />
  </div>
</template>

<script>
import Header from '../components/Home/Header'
import About from '../components/Home/About'
import Road from '../components/Home/Road'
import Feedback from '../components/Home/Feedback'
import Equipment from '../components/Home/Equipment'
import Experience from '../components/Home/Experience'
import Hut from '../components/Home/Hut'
import Footer from '../components/Home/Footer'
import Animation from "~/components/assets/Animation"
export default {
    head: {
    title: 'Spływy kajakowe kaszuby, kajakiem przez Wdę, Zbyrzyce | Kajax Lipusz',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Niezapomniane spływy kajakowe rzeką Wdą i Zbrzyce! Wypożycz nasze kajaki i zwiedź najpopularniejsze kaszubskie szlaki. Noclegi w domku Lipusz'
      }
    ],
  },
  components:{
    Header,
    About,
    Road,
    Feedback,
    Equipment,
    Experience,
    Footer,
    Hut,
    Animation
  },
    methods: {
        runAnimation(){
            let imageColumn = document.querySelector('#about-tile-image-small')
            let imageColumnBig = document.querySelector('#about-tile-image-big') 
            let aboutDescription = document.querySelector('#aboutDescription')
            let feedbackContainer = document.querySelector('#feedbackContainer')
            let equipmentContainer = document.querySelector('[data-animation-id="equipment"]')  
            let experienceContainer = document.querySelector('[data-animation-id="experience"]')
            let hutContainer = document.querySelector('[data-animation-id="hut"]')  
            let lastKnownScrollPosition = 0;
            document.addEventListener('scroll',()=>{
                lastKnownScrollPosition = window.scrollY
             Animation.methods.addAnimation({
                       element: aboutDescription,
                       elementToAnimate: aboutDescription,
                       classNameNew:'animation--fadeInUp',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: imageColumnBig,
                       elementToAnimate: imageColumnBig.querySelector('img'),
                       classNameNew:'tile-animate-full',
                       classNameOld:'tile-animate-small',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: imageColumn,
                       elementToAnimate: imageColumn.querySelector('img'),
                       classNameNew:'tile-animate-full',
                       classNameOld:'tile-animate-small',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: feedbackContainer,
                       elementToAnimate: feedbackContainer.children[0],
                       classNameNew:'animation--fadeInUp',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:200,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: equipmentContainer,
                       elementToAnimate: equipmentContainer.querySelector('[data-animation-id="equipment-main-image"]'),
                       classNameNew:'animation--fadeInLeftToRight',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:300,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: equipmentContainer,
                       elementToAnimate: equipmentContainer.querySelector('[data-animation-id="equipment-specs"]'),
                       classNameNew:'animation--fadeInUp',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:300,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: equipmentContainer,
                       elementToAnimate: equipmentContainer.querySelector('[data-animation-id="equipment-preview"]'),
                       classNameNew:'animation--fadeInRightToLeft',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:300,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: experienceContainer,
                       elementToAnimate: experienceContainer.querySelector('[data-animation-id="experience-wrapper"]'),
                       classNameNew:'animation--fadeInLeftToRight',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: hutContainer,
                       elementToAnimate: hutContainer.querySelector('[data-animation-id="hut-content"]'),
                       classNameNew:'animation--fadeInLeftToRight',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:200,
                       scrollPosition: lastKnownScrollPosition

                   })  
            Animation.methods.addAnimation({
                       element: hutContainer,
                       elementToAnimate: hutContainer.querySelector('[data-animation-id="hut-image"]'),
                       classNameNew:'animation--fadeInLeftToRight',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:200,
                       scrollPosition: lastKnownScrollPosition

                   })
                   




                   
            })
        }
    },
    mounted() {
        this.runAnimation()
    },
}
</script>

<style>
*{
  font-family: 'Montserrat';
}
.animation--fadeInUp{
    animation: fadeInUp 0.9s 0s both cubic-bezier(.27,.11,.65,1.37);
}
.animation--fadeInRightToLeft{
    animation: fadeInRightToLeft 0.9s 0s both cubic-bezier(.27,.11,.65,1.37);
}
.animation--fadeInLeftToRight{
    animation: fadeInLeftToRight 0.9s 0s both cubic-bezier(.27,.11,.65,1.37);
}
.animation--hidden{
    visibility: hidden;
}
@keyframes fadeInUp {
    from {
        opacity: 0;
        -webkit-transform: translate3d(0, 100%, 0);
        transform: translate3d(0, 100%, 0);
    }
    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}

@keyframes fadeInRightToLeft {
    from {
        opacity: 0;
        -webkit-transform: translate3d(100%, 0, 0);
        transform: translate3d(100%, 0, 0);
    }
    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}

@keyframes fadeInLeftToRight {
    from {
        opacity: 0;
        -webkit-transform: translate3d(-100%, 0, 0);
        transform: translate3d(-100%, 0, 0);
    }
    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}
</style>
