<template>
  <div class="">
    <div  class="mb40">
<!--    <footer style="background: #ffffff; padding: 50px 0; margin-bottom:20px;display: flex;justify-content: center" class="footer">-->
<!--      <div class="header-top__logo">-->
<!--        <p class="header-top__logo-p1"><span class="color-dark">LIDER</span>.PRESS</p>-->
<!--        <p class="header-top__logo-p2 color-dark"> Портал по борьбе с инфоцыганством</p>-->
<!--      </div>-->

<!--    </footer>-->
     <div style="grid-gap: 3px; background: #F5F5F5; max-width: 1120px; margin: 0 auto;"  class=" grid gridx2 mb20">
          <div style="padding: 50px 80px 30px 50px" :style="{'background':item.bg }" v-for="item in top2_row" :key="item.title" class="grid-item">
            <p class="color-dark fs-18 mb15">{{item.title}}</p>
            <p class="fs-12 color-dark mb25">{{item.text}}</p>
            <p class="fs-12 color-grey text-up">info@lider.press</p>
          </div>
        </div>

  </div>
    <div style="text-align: center"><p class="text-up fs-14 mb40">Created by:   <span class="text-bold">Webtouch.studio</span></p></div>
  </div>


</template>

<script>
  export default {

    data() {
      return {

        top2_row:[
          {
            bg:'#ffffff',
            title:'Оказались в списке несправедливо?',
            text:'Напишите нам на почту письмо с пометкой “Арбитраж” - мы обязательно разберемся в чем дело'
          },
          {
            bg:'#ffffff',
            title:'Для вопросов и предложений по работе портала',
            text:'Есть идея как улучшить наш сайт? У вас есть материалы, которые нам помогут? Пишите нам на почту, мы все изучим и примим меры!'
          }



        ],
      }
    },

  }
</script>
