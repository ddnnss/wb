<template>
  <div>
    <section>
      <div class="container">
        <el-link href="/posts" class="text-bold color-grey fs-14 mb25"><i class="el-icon-arrow-left el-icon--left"></i>Назад ко всем статьям </el-link>
        <el-card style="padding: 0" class="box-card mb25" shadow="never">
          <img class="mb25" :src="post.image_post" alt="">
          <div style="padding: 0 80px" class="mb25">

            <p class="fs-24 text-bold color-dark mb25">{{post.name}}</p>
            <p class="fs-14 color-dark" v-html="post.text">

            </p>


          </div>
          <div style="padding: 0 80px" class="b-flex">
            <p class="fs-18">{{new Date(post.created_at).toLocaleDateString()}}</p>
            <div class="tag-list">
              <p class="fs-14 text-bold text-up" v-for="tag in post.tags"  :key="tag.id">#{{tag.name}}</p>
            </div>
          </div>



        </el-card>

        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>Ваш комментарий</span>

          </div>

          <div class="b-flex">
            <el-avatar :size="'small'" src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png"></el-avatar>
            <el-input
              style="width: 90%"
              class="mb10"
              type="textarea"
              :autosize="{ minRows: 3, maxRows: 10}"
              placeholder=""
              v-model="textarea2">
            </el-input>
          </div>
          <div style="text-align: end" class="">
            <el-button type="info" icon="el-icon-edit">Отправить</el-button>
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
    async asyncData({$axios,params}){
      console.log(params)
      try{
        const response_unit = await $axios.get(`/api/v1/post/${params.name_slug}`)
        const post = response_unit.data

        return {post}
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

