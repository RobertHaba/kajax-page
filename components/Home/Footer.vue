<template>
    <footer class="footer" id="kontakt"> 
        <div class="footer-layout">
            <div class="column">
                <div class="column-wraper">
                    <div class="footer-about">
                        <h2 class="footer-about-title">Kajax - Kajaki na kaszubach.</h2>
                        <p class="footer-about-description">
                            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam
                        </p>
                    </div>
                    <div class="footer-social">
                        <div class="footer-social-box">
                            <div class="footer-social-box-image-container">
                                <img class="footer-social-box-image-container__image" src="../../assets/facebook.svg" alt="" width="50px" height="50px">
                            </div>
                            <a class="footer-social-box__link" href="https://www.facebook.com/Kajax-Sp%C5%82ywy-kajakowe-342252465837367/">Facebook</a>
                        </div>
                        <div class="footer-social-box">
                            <div class="footer-social-box-image-container">
                                <img class="footer-social-box-image-container__image" src="../../assets/google.svg" alt="" width="50px" height="50px">
                            </div>
                            <a class="footer-social-box__link" href="https://goo.gl/maps/xwBYrLZ6YnhoiUVM7">Google</a>
                        </div>
                    </div>
                    <div class="footer-shortcuts" v-if="roads !== ''">
                        <h3 class="footer-shortcuts-title">Skróty:</h3>
                        <ul class="footer-shortcuts-list">
                            <li class="footer-shortcuts-list__item" v-for="road in roads" :key="road.id">
                                <nuxt-link :to="`/road/${road.title}-${road.id}`">Trasa kajakowa - {{road.subtitle}}, rzeką {{road.title}}</nuxt-link>
                            </li>
                            <li class="footer-shortcuts-list__item"><nuxt-link to="/hut">Domek Holenderski</nuxt-link></li>
                        </ul>
                    </div>
                </div>
            </div>
            <div class="column column--right">
                <div class="footer-map-container">
                    <iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d9359.261048744675!2d17.7864533!3d54.0947507!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x37ba492c8cfd86df!2sWypo%C5%BCyczalnia%20kajak%C3%B3w%20&#39;&#39;KAJAX&#39;&#39;!5e0!3m2!1spl!2spl!4v1616359697344!5m2!1spl!2spl" max-width="500" width="100%" height="320" style="border:0; border-radius:10px" allowfullscreen="" loading="lazy" title="Mapa - Lokalizacja firmy Kajax"></iframe>
                </div>
                <div class="footer-contact">
                        <ul class="footer-contact-list">
                            <li class="footer-contact-list__item"><h4 class="footer-contact-list-item-title">Numer telefonu:</h4><p class="footer-contact-list-item-text"><a href="tel:+48696599556">696-599-556</a></p></li>
                            <li class="footer-contact-list__item"><h4 class="footer-contact-list-item-title">Adres:</h4><p class="footer-contact-list-item-text">Pomorze - Lipusz 83-424, ul. Rogali 9</p></li>
                        </ul>
                    
                </div>
            </div>
        </div>
        <div class="footer-copyright">
            <p class="copyright-text">Copyright © siteman.com dla kajakinakaszubach.pl 2021</p>
        </div>
    </footer>
</template>

<script>
import roadFooter from '~/apollo/queries/home/road-footer'
export default {
    data(){
        return{
            roads:''
        }
    },
    apollo:{
        roads:{
            prefetch:true,
            query:roadFooter,
        }
    }
}
</script>

<style scoped>
.footer{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
    padding: 5rem;
    background-color: #005492;
    color:#FFF;

}
.footer-layout{
    display: flex;
    align-items: stretch;
    justify-content: stretch;
    width: calc(100% + 1rem);
    max-width: 1300px;
    min-height: 500px;
    margin:0 auto;
    margin: -1rem 0 0 -1rem;
}
.column{
    display: flex;
    width: 100%;
    height: 100%;
    margin: 1rem 0 0 1rem;
}
.column--right{
    flex-direction: column;
    align-items: flex-end;
}
.column-wraper{
    max-width: 380px;
}
.footer-about-title{
    font-size: 1.4rem;
    margin-bottom: 0.8rem;
}
.footer-about-description{
    color:#b5cddb;
}
.footer-social{
    display: flex;
    justify-content: space-evenly;
    margin: 3rem 0;
}
.footer-social-box{
    display: flex;
    align-items: center;
    flex-direction: column;
}
.footer-social-box-image-container{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50px;
    width: 50px;
    background-color: #FFF;
    border-radius: 100px;
}
.footer-social-box-image-container__image{
    width: 100%;
    max-width: 25px;
    height: 100%;
    max-height: 25px;
}
.footer-social-box__link{
    margin-top: 0.5rem;
    font-size: 0.9rem;
}
.footer-shortcuts-title{
    margin-bottom: 1rem;
    font-size: 1.2rem;
}
.footer-shortcuts-list{
    display: flex;
    flex-direction: column;
    border-left: 1px solid #FFF;
}
.footer-shortcuts-list__item{
    position: relative;
    margin-bottom: 0.4rem;
    padding: 0 1rem;
    color: #b5cddb;
}
.footer-shortcuts-list__item::after{
    content: '';
    position: absolute;
    top:0.5rem;
    left: -2.8px;
    width: 5px;
    height: 5px;
    background-color: #FFF;
    border-radius: 100%;
}
.footer-map-container{
    width: 100%;
    max-width: 500px;
    height: 320px;
    background-color: #FFF;
    border-radius: 20px;
}
.footer-contact{
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    margin-top: 2rem;
    padding: 0.5rem;
    width: 100%;
    max-width: 500px;
}
.footer-contact-list{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
.footer-contact-list__item{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 0.6rem;
}
.footer-contact-list-item-title{
    margin-bottom: 0.3rem;
}
.footer-contact-list-item-text{
    padding: 0.3rem 1rem;
    font-size: 0.8rem;
    font-weight: bold;
    color:#005492;
    background-color: #FFF;
    border-radius: 100px;
}
.footer-copyright{
    display: flex;
    margin:0 auto;
    margin-top: 1rem;
    width: 100%;
    max-width: 1300px;
}
.copyright-text{
    padding: 0.5rem 2rem;
    color: #005492;
    font-size: 0.9rem;
    font-weight: bold;
    background-color: #FFF;
    border-radius: 100px;

}
@media screen and (max-width:950px) {
    .footer-layout{
        flex-direction: column;
    }
    .column-wraper{
        width: 100%;
        max-width: 100%;
    }
    .column-wraper,
    .column--right{
        align-items: center;
    }
    .footer-copyright{
        justify-content: center;
    }
}
@media screen and (max-width:500px) {
    .footer{
        padding: 5rem 2rem;
    }
    .footer-layout{
        width: 100%;
        margin: 0;
    }
    .column{
        margin: 0;
    }
    .column--right{
        margin-top: 3rem;
    }
    .footer-copyright{
        margin-top: 3rem;
    }
}
</style>
