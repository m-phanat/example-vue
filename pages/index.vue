<template>
  <b-container fluid>
    <b-row>
      <b-col style="margin-top:10px">
        <b-form-file
          v-model="file"
          :state="Boolean(file)"
          placeholder="Choose a file or drop it here..."
          drop-placeholder="Drop file here..."
        ></b-form-file>
      </b-col>
    </b-row>
    <b-row style="margin-top:10px" class="text-center">
      <b-col>
        <b-button variant="success" v-on:click="submitFile()">Submit</b-button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      file: null
    }
  },
  methods: {
    async testAxios() {
      const ip = await this.$axios.$get('http://localhost:8082/')
      console.log(ip)
    },

    submitFile() {
      /*
                Initialize the form data
            */
      let formData = new FormData()

      /*
                Add the form data we need to submit
            */
      formData.append('file', this.file)

      /*
          Make the request to the POST /single-file URL
        */
      this.$axios
        .$post('http://localhost:8082/upload', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        })
        .then(function () {
          alert('SUCCESS!!')
        })
        .catch(function () {
          alert('FAILURE!!')
        })
    },

    /*
        Handles a change on the file upload
      */
    handleFileUpload() {
      this.file = this.$refs.file.files[0]
    }
  },
  mounted() {
    this.testAxios()
  }
}
</script>

<style></style>
