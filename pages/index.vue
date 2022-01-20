<template>
  <div class="bg">
    <b-container>
      <b-row>
        <b-col cols="12" class="p-3" style="margin-top: 20vh">
          <b-img src="/woman.png" alt="Left image" fluid></b-img>
        </b-col>
      </b-row>
      <b-row class="mt-4">
        <b-col cols="12" class="text-center">
          <h2>Article</h2>
        </b-col>
      </b-row>
      <b-row class="mt-5 mb-5">
        <b-col sm class="text-center mb-4">
          <b-link style="color: black" to="/article">
            <b-img src="/image1.png" alt="Left image" fluid></b-img>
            <div class="title text-left">
              How to create meaningful progress with design?
            </div>
            <div class="subtitle text-left">
              It takes hard work to find the balance between values and aims.
            </div>
          </b-link>
        </b-col>
        <b-col sm class="text-center mb-4">
          <b-img src="/image2.png" alt="Left image" fluid></b-img>
          <div class="title text-left">
            Is It Ok to Cheat to be a Better UX/UI Designer?
          </div>
          <div class="subtitle text-left">
            How can cheating in design help you become a better designer?
          </div>
        </b-col>
        <b-col sm class="text-center mb-4">
          <b-img src="/image3.png" alt="Left image" fluid></b-img>
          <div class="title text-left">
            Try peak-end rule on user journey map
          </div>
          <div class="subtitle text-left">
            Designing a user flow requires careful management of resources.
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
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
