<template>
  <div>
  <section>
    <div class="container">
        <el-link href="/list" class="text-bold color-grey fs-14 mb25"><i class="el-icon-arrow-left el-icon--left"></i>Назад к черному списку </el-link>

      <el-card class="box-card" shadow="never">
        <div style="text-align: center" class="">
          <img :src="item.image" alt="">
          <p class="fs-24 color-dark">{{item.name}}</p>
<!--          <p class="color-dark">{{item.type.name}}</p>-->
          </div>
          <el-divider></el-divider>
        <div style="padding: 0 140px">
               <p class="fs-14 color-grey-card mb15">Подробности</p>
          <p class="mb25" v-html="item.details"></p>

        </div>

          <el-divider></el-divider>
        <div style="padding: 0 140px">
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Дата добавления</p>
          <p>{{new Date(item.created_at).toLocaleDateString()}}</p>
        </div>
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Контакты</p>
          <p>{{item.contact}}</p>
        </div>

        </div>
         <el-divider></el-divider>
        <div style="padding: 0 140px">
          <div style="display: flex; flex-wrap: wrap">
          <p class="fs-14 color-grey-card mb15" style="flex-basis: 300px">Пруфы</p>
          <p  v-html="item.proofs"></p>
        </div>
        </div>




      </el-card>
    </div>
  </section>




  </div>

</template>

<script>
  export default {
    async asyncData({$axios,params}){
      console.log(params)
      try{
        const response_unit = await $axios.get(`/api/v1/bl/item/${params.name_slug}`)
        const item = response_unit.data
        console.log(item)
        return {item}
      }catch (e) {
        throw e
      }
    },
    data() {
      return {
        textarea2:'',
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

