<template>
  <div>
    <my-upload :field="temp.fileInputName"
               @crop-success="cropSuccess"
               @crop-upload-success="cropUploadSuccess"
               @crop-upload-fail="cropUploadFail"
               v-model="show"
               :width="300"
               :height="300"
               :noRotate="false"
               :withCredentials="false"
               :url="temp.uploadUrl"
               :params="temp.bodies"
               :headers="temp.headers"
               img-format="png">

    </my-upload>
    <span @click="toggleShow" >
      <slot name="uploadBtn">
      </slot>
    </span>
    </div>
</template>
<script>
  import myUpload from 'vue-image-crop-upload'
  import axios from 'axios'
  export default {
    props: ['serviceUrl', 'token'],
    data() {
      return {
        temp: {
          method: '',
          uploadUrl: '',
          fileInputName: '',
          bodies: {},
          headers: {}
        },
        show: false
      }
    },
    components: {
      myUpload
    },
    name: 'avatarUpload',
    methods: {
      toggleShow() {
        this.show = !this.show
        if (this.show) {
          axios.get(this.serviceUrl, {
            params: {
              mimeType: 'png'
            },
            headers: {
              Authorization: 'Bearer ' + this.token
            }
          })
            .then((response) => {
              this.temp = response.data.data
              /*
              method: '',
                uploadUrl: '',
                fileInputName: '',
                bodies: {},
              headers: {}
              this.temp.method = response.data.data.method
              this.temp.uploadUrl = response.data.data.uploadUrl
              this.temp.fileInputName = fileInputName
              */
            })
        }
      },
      /**
       * crop success
       *
       * [param] imgDataUrl
       * [param] field
       */
      cropSuccess(imgDataUrl, field) {
        // console.log('-------- crop success --------')
        console.log(arguments)
        console.log(arguments)
        this.imgDataUrl = imgDataUrl
      },
      /**
       * upload success
       *
       * [param] jsonData  server api return data, already json encode
       * [param] field
       */
      cropUploadSuccess(jsonData, field) {
        // console.log('-------- upload success --------')
        // console.log(jsonData, field)
        // console.log('field: ' + field)
        this.$emit('successUpload', {
          jsonData,
          field,
          imgUrl: this.imgDataUrl
        })
      },
      /**
       * upload fail
       *
       * [param] status    server api return error status, like 500
       * [param] field
       */
      cropUploadFail(status, field) {
        // console.log('-------- upload fail --------')
        // console.log(status)
        // console.log('field: ' + field)
        this.$emit('failUpload', {
          status,
          field,
          imgUrl: this.imgDataUrl
        })
      }
    }
  }
</script>
