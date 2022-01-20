<template>
  <div class="bg">
    <b-container style="margin-top: 20vh">
      <b-row class="mt-5 mb-5">
        <b-col
          v-for="dataArticles in dataArticle"
          :key="dataArticles.id"
          lg="4"
          md="6"
          sm="12"
          class="text-center mb-4"
        >
          <b-link style="color: black" :to="'/article/' + dataArticles.id">
            <b-img :src="dataArticles.image" alt="Left image" fluid></b-img>
            <div class="title text-left">
              {{ dataArticles.title }}
            </div>
            <div class="subtitle text-left">
              {{ dataArticles.short_description }}
            </div>
          </b-link>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'Article',
  data() {
    return {
      title: '',
      shortdesc: '',
      image: '',
      dataArticle: [],
    }
  },
  mounted() {
    this.getArticle()
  },
  methods: {
    async getArticle() {
      await this.$axios
        .get('/api/article?search=&size=21&page=1', {
          headers: { Authorization: 'Bearer ' + this.$cookies.get('token') },
        })
        .then((response) => {
          // console.log(response.data.content)
          const dataFilter = response.data.content.filter(
            (el) =>
              el.image.includes('.png') ||
              el.image.includes('.jpeg') ||
              el.image.includes('.jpg')
          )
          this.dataArticle = dataFilter
          console.log('filter data', this.dataArticle)
        })
        .catch((err) => {
          if (!err) {
          } else {
            console.log(err.response.data)
            console.log(err.response.status)
            console.log(err.response.headers)
            // this.resetLoginForm()
            if (err.response.status === 409) {
              this.$toast.error(err.response.data.message.details[0].message)
            } else {
              this.$toast.error(err.response.data.message)
            }
          }
        })
    },
  },
}
</script>
<style scoped>
.bg {
  background-color: #ffffff;
}
.title {
  font-family: Roboto;
  font-style: normal;
  font-weight: 500;
  font-size: 24px;
  margin-bottom: 8px;
  margin-top: 16px;
}
.subtitle {
  font-family: Roboto;
  font-style: normal;
  font-weight: 300;
  font-size: 16px;
}
</style>
