<template>
  <div>

    <section>
      <div class="container">
        <el-card class="box-card mb25" shadow="never">
          <div class=" b-flex a-bt">
            <div class="mb10">
              <p class="fs-14 color-grey-card mb10">Фильтрация по типу</p>
              <el-select  v-model="black_list_type" @change="typeChange" placeholder="Выберите">
                <el-option

                  :key="0"
                  :label="'ВСЕ'"
                  :value="'all'">
                </el-option>
                <el-option
                  v-for="item in black_list_types"
                  :key="item.id"
                  :label="item.name"
                  :value="item.id">
                </el-option>
              </el-select>
            </div>


            <div class="mb10">
              <p class="fs-14 color-grey-card mb10">Введите для поиска имя\телефон\сайт...</p>
              <el-input placeholder="" v-model="search"></el-input>

            </div>
            <div class="mb10">
              <el-button type="info" @click="searchItems" icon="el-icon-search">Искать</el-button>
            </div>
          </div>

        </el-card>


       <el-table
         ref="bl"
          :data="black_list"
          @current-change="handleCurrentChange"
          style="width: 100%" >
          <el-table-column
            prop="id"
            label="ID"
            width="50">

          </el-table-column>
          <el-table-column
            prop="image"
            label="Фото"
            width="100">
            <template slot-scope="scope">
              <img :src="scope.row.image" alt="">
            </template>
          </el-table-column>
          <el-table-column
            prop="type.name"
            label="Тип"
            width="150"
          >
          </el-table-column>
          <el-table-column
            prop="name"
            label="Название"
            width="150">
          </el-table-column>
          <el-table-column
            prop="reason"
            label="Причина добавления">
          </el-table-column>
          <el-table-column
            prop="contact"
            label="Контакты"
            width="200">

          </el-table-column>
        </el-table>


      </div>
    </section>
<!--     <section>-->
<!--      <div class="container">-->

<!--        <div class="grid gridx2">-->
<!--          <div style="padding: 80px 50px" :style="{'background':item.bg }" v-for="item in top2_row" :key="item.title" class="grid-item">-->
<!--            <p class="text-bold color-dark fs-24 mb15">{{item.title}}</p>-->
<!--            <p class="fs-14 color-dark">{{item.text}}</p>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </section>-->




  </div>

</template>
<script>
  export default {
    async asyncData({$axios,params}){
      try{
        const  response_posts = await $axios.get(`/api/v1/posts_t/?tag=0`)
        const  response_tags = await $axios.get(`/api/v1/tags/`)
        const  response_bl = await $axios.get(`/api/v1/bl/`)
        const  response_bl_types = await $axios.get(`/api/v1/bl/types/`)

        const posts = response_posts.data.results
        const black_list = response_bl.data.results
        const black_list_types = response_bl_types.data.results
        const total_pages = response_posts.data.page_count - 1
        const tags = response_tags.data.results
        const url = response_posts.data.links.next

        return {
          posts,
          tags,
          black_list,
          black_list_types,
          total_pages,
          url
        }
      }catch (e) {
        throw e
      }

    },
    data() {
      return {

        black_list_type: '',
        value1: '',
        search: '',
        currentRow: null,
        cur_tag:0,
        top_row:[
          {
            image:'/t1.png',
            title:'Кто мы?',
            text:'Мы - команда Андрея Ковалева'
          },
          {
            image:'/t2.png',
            title:'Что делаем?',
            text:'Разоблачаем инфоцыган и формируем специальный черный список'
          },
          {
            image:'/t3.png',
            title:'Зачем и почему?',
            text:'Потому что хочется так'
          },


        ],
        top1_row:[
          {
            bg:'#E2E6F4',
            title:'Наша роль',
            text:'Отбирать материал, формировать доказательную базу с информацией и вносить негативных персонажей (личностей или фирм) в наш черный список'
          },
          {
            bg:'#BEDCF8',
            title:'Ваша роль',
            text:'Отправлять нам на почту материалы для расследований, писать свое мнение на форуме, делиться информацией с друзьями и близкими чтобы избежать мошенничества'
          }



        ],
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
    },
    methods:{
      pageChange(val){
        this.getPosts(this.cur_tag,val)
      },
      async searchItems(){
         await this.$axios.get(`/api/v1/bl/search?query=${this.search}`)
          .then((response) => {
            console.log(response.data);
            this.black_list = response.data.results
          })
          .then(response => {
            console.log('response1')
            console.log(response)
          })
          .catch(error => {
            console.log('response2')
            console.log(error.response)
            this.step1_btn_loading = false
            this.login_error = true

          });
      },
      async typeChange(){

        await this.$axios.get(`/api/v1/bl/filter?type=${this.black_list_type}`)
          .then((response) => {
            console.log(response.data);
            this.black_list = response.data.results
          })
          .then(response => {
            console.log('response1')
            console.log(response)
          })
          .catch(error => {
            console.log('response2')
            console.log(error.response)
            this.step1_btn_loading = false
            this.login_error = true

          });
      },
      handleCurrentChange(val) {
        console.log(val)
        this.currentRow = val;
        this.$router.push(`/list/${val.name_slug}`).catch(()=>{})
      }

    }
  }
</script>


