<template>
  <div>
  <section>
    <div class="container">
      <el-card class="box-card" shadow="never">
        <div style="text-align: center" class="">
          <img src="http://placehold.it/330x260" alt="">
          <p class="fs-24 color-dark">ООО “ЮНИКОР”</p>
          <p class="color-dark">IT Компания</p>
          </div>
          <el-divider></el-divider>
        <div style="padding: 0 140px">
               <p class="fs-14 color-grey-card mb15">Подробности</p>
          <p class="mb25">Начиная с 2013 года данная компания совершила массу нарушей и кидания людей по теме разработки того и сего, а так же изволится пятого и десятого, сотого и двухсотого, десерта и обеда, редиски и морковки, блинов и торотов.</p>
          <p>Общая сумма нарушений: <b>20.000$</b></p>

        </div>

          <el-divider></el-divider>
        <div style="padding: 0 140px">
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Дата добавления</p>
          <p>01.04.2020</p>
        </div>
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Контакты</p>
          <p>unicokr.ru, +79169991234</p>
        </div>

        </div>
         <el-divider></el-divider>
        <div style="padding: 0 140px">
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Пруфы</p>
          <p>Статья на хабре про данного персонажа<br>habr.ru\49235912<br><br>Видеоролик от канала “LiveDoiki”<br>youtube.com\triiaji</p>


        </div>
        </div>




      </el-card>
    </div>
  </section>
   <section>
      <div class="container">

        <div class="grid gridx2">
          <div style="padding: 80px 50px" :style="{'background':item.bg }" v-for="item in top2_row" :key="item.title" class="grid-item">
            <p class="text-bold color-dark fs-24 mb15">{{item.title}}</p>
            <p class="fs-14 color-dark">{{item.text}}</p>
          </div>
        </div>
      </div>
    </section>



  </div>

</template>

<script>
  export default {
    data() {
      return {
top2_row:[
          {
            bg:'#ffffff',
            title:'Оказались в списке случайно?',
            text:'Добро пожаловать в арбитраж'
          },
          {
            bg:'#ffffff',
            title:'Вопросы по работе сайта?',
            text:'Мы - команда энтузиастов, осуществляем и реализовываем проект известного многим людям бизнесмена и разоблачителя Андрея Ковалева'
          }



        ],

      }
    }
  }
</script>

