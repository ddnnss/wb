<template>
  <div>
    <section>
      <div class="container">

       <el-row :gutter="15">
          <el-col :xs="24" :sm="12" :md="8" :lg="6" :xl="6">
            <el-card style="padding: 50px 45px" class="box-card mb25 no-border" shadow="never" >

              <ul>
                <li><el-link class="color-dark mb40" @click="getPosts(0,1)" :class="{textBold : cur_tag===0}">ВСЕ ПОДРЯД</el-link></li>
                <li v-for="tag in tags" :key="tag.id"><el-link @click="getPosts(tag.id,1)"
                                                               :class="{textBold : cur_tag===tag.id}"
                                                               class="text-up  color-l-grey fs-14">#{{tag.name}}</el-link></li>

              </ul>


            </el-card>
          </el-col>
          <el-col :xs="24" :sm="12" :md="16" :lg="18" :xl="18">
            <el-card style="padding: 0" class="mb15  no-padding" shadow="hover" v-for="post in posts" :key="post.id">

                 <div class="card-inner">
                <img :src="post.image" alt="">

                <div class="card-inner__div">
               <nuxt-link :to="'/posts/'+post.name_slug">
                   <p class="fs-18 mb15 color-dark text-bold" >{{post.name}}</p>
                </nuxt-link>
                  <p class="fs-14 mb25">{{post.short_description}}</p>
                  <div class="b-flex">
                    <p class="fs-12 color-dark">{{new Date(post.created_at).toLocaleDateString()}}</p>
                    <div class="tag-list">
                       <el-link class="fs-12 color-dark text-up" v-for="tag in post.tags" @click="getPosts(tag.id,1)" :key="tag.id" >#{{tag.name}}</el-link>
                    </div>


                  </div>
                </div>
              </div>


            </el-card>

            <el-pagination
              :hide-on-single-page="true"
  background
  layout="prev, pager, next"
  :page-count="total_pages"
  @current-change="pageChange"
            >

</el-pagination>


          </el-col>
        </el-row>

      </div>

    </section>





  </div>

</template>

<script>
  export default {
    async asyncData({$axios,params}){
      try{
        const  response_posts = await $axios.get(`/api/v1/posts_t/?tag=0`)
        const  response_tags = await $axios.get(`/api/v1/tags/`)
        const  response_bl = await $axios.get(`/api/v1/bl/`)

        const posts = response_posts.data.results
        const black_list = response_bl.data.results
        const total_pages = response_posts.data.page_count - 1
        const tags = response_tags.data.results
        const url = response_posts.data.links.next

        return {
          posts,
          tags,
          black_list,
          total_pages,
          url
        }
      }catch (e) {
        throw e
      }

    },
    data() {
      return {

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
      async getPosts(tag_id,page){
          await this.$axios.get(`/api/v1/posts_t/?tag=${tag_id}&page=${page}`)
          .then((response) => {
            console.log(response.data);
            this.url = response.data.links.next
            this.total_pages = response.data.page_count -1
            this.posts = response.data.results
            this.cur_tag = tag_id
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

      }
    }
  }
</script>

