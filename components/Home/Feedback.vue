<template>
  <section class="container" id="feedbackContainer">
    <div class="feedback-container" >
      <div class="feedback-header">
          <div class="feedback-card feedback-card--small">
            <h2 class="feedback-main-title">OPINIE</h2>
          </div>
          <p class="feedback-main-text">Spodobały Ci się nasze spływy? Oceń nas!</p>
          <div class="feedback-main-social-container">
            <a href="https://www.facebook.com/Kajax-Spływy-kajakowe-342252465837367" class="feedback-main-social-button"><img src="../../assets/facebook.svg" alt="Facebook icon as button"></a>
            <a href="https://goo.gl/maps/xwBYrLZ6YnhoiUVM7" class="feedback-main-social-button"><img src="../../assets/google.svg" alt="Facebook icon as button"></a>
          </div>
      </div>
      <div class="feedback-card">
            <div class="feedback-card-content">
                <h2 class="feedback-card-title">Google</h2>
                <p class="feedback-card-name">Marta</p>
                <p class="feedback-card-text">Bardzo sympatyczny właściciel, kajaki przygotowane, czyste, szybko, sprawnie, ceny umiarkowane. Polecam</p>
            </div>
            <p class="feedback-card-footer">
              Wrzesień
            </p>
        </div>
        <div class="feedback-card">
            <div class="feedback-card-content">
                <h2 class="feedback-card-title">Google</h2>
                <p class="feedback-card-name">Charlotte</p>
                <p class="feedback-card-text">Szybki, rzeczowy i przemiły kontakt z właścicielem, spływ rzeką Wdą na trasie Lipusz - Wdzydze Kiszewskie rewelacyjny, sprzęt w bardzo dobrym stanie, naprawdę polecam.</p>
            </div>
            <p class="feedback-card-footer">
              Sierpień
            </p>
        </div>
        <div class="feedback-card">
            <div class="feedback-card-content">
                <h2 class="feedback-card-title">Google</h2>
                <p class="feedback-card-name">Krzysztof</p>
                <p class="feedback-card-text">Dobry dojazd , jest tam parking i WC ,to atut firmy każdy telefon odebrany miła konkretna zozmowa .
Zamówiłam kajak w ciągu tygodnia i kiedy dojechałem już na mnie czekał czysty .
Ja osobiście polecam.</p>
            </div>
            <p class="feedback-card-footer">
              Wrzesień
            </p>
        </div>
    </div>
  </section>
</template>

<script>
export default {
}
</script>

<style scoped>
.container{
  position: relative;
  z-index: 0;
  min-height: 600px;
  background-color: #F5F5F5;
  padding: 7rem 5rem;
}
.feedback-container{
  position: relative;
  z-index: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  max-width: 1300px;
  margin:0 auto;
}
.container::after{
  content: '';
  position: absolute;
  overflow: hidden;
  top:8rem;
  left: 0;
  right: 200px;
  z-index: -1;
  height: 120px;
  background-color: #EAEAEA;
}
.feedback-header{
  display: flex;
  flex-direction: column;
  width: 200px;
  height: 400px;
}
.feedback-card{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 290px;
  height: 400px;
  padding: 2rem 2rem;
  background: #FCFCFC;
  box-shadow: 0px 0px 8px rgba(218, 218, 218, 0.616);
  border-radius: 15px;
}
.feedback-card--small{
  justify-content: flex-end;
  width: 200px;
  height: 250px;
  background: #4581B8;
  color: #FFF;
}
.feedback-main-title{
  font-size: 2rem;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}
.feedback-main-social-container{
  display: flex;
  justify-content: space-evenly;
}
.feedback-main-social-button{
  width: 25px;
  height: 25px;
}
.feedback-main-social-button img{
  width: 100%;
  height: 100%;
}
.feedback-main-text{
  padding:1.5rem 1rem;
  color: #000;
  font-weight: bold;
  text-align: center;
}
.feedback-card-title{
  padding-bottom: 1.5rem;
  font-size: 2.1em;
  font-weight: bold;
  color: #999999;
  text-align: center;
}
.feedback-card-name{
  font-weight: bold;
  font-size: 1.1rem;
  padding-bottom: 1.5rem;
  color:#4A4A4A;
}
.feedback-card-text{
  font-size: 0.85rem;
  color:#4A4A4A;
}
.feedback-card-footer{
  padding-top: 1rem;
  border-top: 1px solid #E0E0E0;
  color: #4581B8;
}
@media screen and (max-width:1300px) {
  .feedback-header{
    width: 100%;
    margin-bottom: 4rem;
  }
  .feedback-main-text, .feedback-main-social-container{
    width: 100%;
    max-width: 290px;
  }
  .container::after{
    right: 0;
  }
  .feedback-card{
    margin: 1rem 0;
  }
  .feedback-card--small{
    margin: 0;
    width: 100%;
    max-width: 290px;
  }
}
@media screen and (max-width:500px) {
  .container{
    padding: 5rem 1rem;
  }
  .feedback-container{
    justify-content: center;
  }
  .feedback-header{
    align-items: center;
  }
}

</style>