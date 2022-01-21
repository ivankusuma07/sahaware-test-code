<template>
  <div class="bg">
    <LoadSpinner v-if="showHideSpinner" />
    <b-container style="margin-top: 5vh">
      <b-row class="mt-5 mb-5">
        <b-col lg="3" sm="2" xs="2"> </b-col>
        <b-col lg="6" sm="8" xs="8">
          <div class="title text-left">
            {{ dataArticle.title }}
          </div>
          <div class="subtitle text-left">
            {{ dataArticle.short_description }}
          </div>
          <b-img :src="dataArticle.image" fluid></b-img>
          <div v-html="htmlarticle" class="text-left mt-5"></div>
        </b-col>
        <b-col lg="3" sm="2" xs="2"> </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'Details',
  data() {
    return {
      title: '',
      shortdesc: '',
      image: '',
      dataArticle: {},
      htmlarticle: '',
    }
  },
  beforeCreate() {
    this.showHideSpinner = true
  },
  created() {
    this.getArticles()
    // console.log(this.$route.params)
  },
  methods: {
    async getArticles() {
      console.log('masuk')
      await this.$axios
        .get(`/api/article/${this.$route.params.id}`, {
          headers: { Authorization: 'Bearer ' + this.$cookies.get('token') },
        })
        .then((response) => {
          this.showHideSpinner = false
          console.log(response.data.content)
          const dataFilter = response.data.content
          this.dataArticle = dataFilter
          console.log('filter data', this.dataArticle)
          this.stringToHTML(this.dataArticle.description)
        })
        .catch((err) => {
          this.showHideSpinner = false
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
    parseHtml() {
      // var t0, t1, html

      // t0 = performance.now();
      // this.htmlarticle = document.implementation.createHTMLDocument('test')
      // t1 = performance.now();

      // this.htmlarticle.documentElement.innerHTML =
      const myHtmlString = this.dataArticle.description
      this.htmlarticle = new DOMParser().parseFromString(
        myHtmlString,
        'text/html'
      )
      // console.log()
      // this.htmlarticle.body.innerHTML
    },
    stringToHTML(str) {
      var parser = new DOMParser()
      var doc = parser.parseFromString(str, 'text/html')
      // console.log(doc.body)
      // return doc.body

      this.htmlarticle = doc.body.outerHTML.replace(/\\"/g, '"')
    },
  },
}
</script>
<style scoped>
.bg {
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.title {
  font-family: Roboto;
  font-style: normal;
  font-weight: 500;
  font-size: 36px;
  margin-bottom: 40px;
  margin-top: 0px;
}
.subtitle {
  font-family: Roboto;
  font-style: normal;
  font-weight: 300;
  font-size: 24px;
  margin-bottom: 40px;
}
</style>
