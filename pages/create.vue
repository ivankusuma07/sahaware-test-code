<template>
  <div class="bg">
    <LoadSpinner v-if="showHideSpinner" />
    <b-container style="margin-top: 10vh">
      <b-row class="mt-5 mb-5">
        <b-col lg="8" md="8" sm="12" class="mb-4">
          <div class="title mb-4">Create New Article</div>
          <b-form-group id="input-group-1" label="Title" label-for="input-1">
            <b-form-input
              id="input-1"
              v-model="formArticle.title"
              type="text"
              placeholder="Enter your article title"
              required
            ></b-form-input>
          </b-form-group>
          <ckeditor
            :editor="editor"
            v-model="formArticle.description"
            :config="editorConfig"
          ></ckeditor>
        </b-col>
        <b-col lg="4" md="4" sm="12" class="mb-4">
          <div class="title mb-4">Publication Detail</div>
          <div class="subtitle mb-2">Short Description</div>
          <b-form-textarea
            id="textarea-no-resize"
            v-model="formArticle.short_description"
            placeholder="Enter your Article Short Description"
            rows="6"
            no-resize
            class="mb-3"
          ></b-form-textarea>
          <div class="subtitle mb-2">Thumbnail</div>
          <b-form-group class="mb-3">
            <b-form-file
              id="file-default"
              v-model="formArticle.image"
            ></b-form-file>
          </b-form-group>
          <div class="subtitle mb-2">Category</div>
          <b-form-select
            v-model="formArticle.category_id"
            :options="selectOptions"
            class="mb-3"
          >
            <template #first>
              <b-form-select-option :value="null" disabled>
                Select Category
              </b-form-select-option>
            </template>
          </b-form-select>
          <b-row class="mb-3">
            <b-col> <div class="subtitle mb-2">Published</div></b-col>
            <b-col class="text-right">
              <b-form-checkbox
                v-model="formArticle.is_visible"
                name="check-button"
                switch
              >
              </b-form-checkbox>
            </b-col>
          </b-row>
          <b-button type="button" variant="danger" @click="publishArticle"
            ><b-spinner v-show="showSpinner" class="mr-2" small></b-spinner
            >Publish</b-button
          >
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import ClassicEditor from '@ckeditor/ckeditor5-build-classic'

export default {
  name: 'Create',
  data() {
    return {
      editor: ClassicEditor,
      editorConfig: {
        // The configuration of the editor.
        toolbar: [
          'heading',
          '|',
          'alignment',
          '|',
          'bold',
          'italic',
          'underline',
          '|',
          'link',
          '|',
          'undo',
          'redo',
        ],
      },
      showHideSpinner: true,
      formArticle: {
        title: '',
        short_description: '',
        description: '<p>Write your story</p>',
        category_id: null,
        is_visible: true,
        image: null,
      },
      selectOptions: [],
      checked: true,
      showSpinner: false,
    }
  },
  beforeCreate() {
    this.showHideSpinner = true
  },
  created() {
    // this.getArticle()
    this.showHideSpinner = false
    this.getArticleCategory()
  },
  watch: {
    formArticle: {
      deep: true,

      // We have to move our method to a handler field
      handler() {
        console.log(this.formArticle)
      },
    },
  },
  methods: {
    async publishArticle() {
      this.showSpinner = true
      console.log(this.formArticle)
      const formData = new FormData()
      Object.keys(this.formArticle).forEach((key) => {
        formData.append(key, this.formArticle[key])
      })
      await this.$axios
        .post(
          '/api/article/create',
          {
            headers: { Authorization: 'Bearer ' + this.$cookies.get('token') },
          },
          formData
        )
        .then((response) => {
          console.log(response.data.content)
          this.showSpinner = false
          this.resetArticlePost()

          // console.log('filter data', this.dataArticle)
        })
        .catch((err) => {
          this.showSpinner = true
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
    async getArticleCategory() {
      await this.$axios
        .get('api/article-category', {
          headers: { Authorization: 'Bearer ' + this.$cookies.get('token') },
        })
        .then((response) => {
          // console.log(response.data.content)

          const oldKey = response.data.content
          this.selectOptions = oldKey.map((el) => {
            return {
              value: el.id,
              text: el.title,
            }
          })
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
    resetArticlePost() {
      this.formArticle = {
        title: '',
        short_description: '',
        description: '<p>Write your story</p>',
        category_id: null,
        is_visible: true,
        image: null,
      }
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
  font-size: 24px;
  margin-bottom: 8px;
  margin-top: 16px;
}
.subtitle {
  font-family: Roboto;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
}
.cke_contents {
  height: 500px !important;
}
</style>
