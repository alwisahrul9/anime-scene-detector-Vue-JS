<template>
  <Navbar />
  <section class="flex justify-center">
    <div class="grid grid-cols-12 border shadow-xl md:px-8 px-4 md:py-12 py-8 mt-16 lg:w-[80%] xl:w-[70%] w-[90%]">
      <div class="lg:col-span-6 mb-16 col-span-12 relative">
        <svg :class="showTrash ? 'w-10 h-10 text-rose-600 absolute top-4 right-4' : 'hidden'" @click="removeImage" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 18 20">
          <path d="M17 4h-4V2a2 2 0 0 0-2-2H7a2 2 0 0 0-2 2v2H1a1 1 0 0 0 0 2h1v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V6h1a1 1 0 1 0 0-2ZM7 2h4v2H7V2Zm1 14a1 1 0 1 1-2 0V8a1 1 0 0 1 2 0v8Zm4 0a1 1 0 0 1-2 0V8a1 1 0 0 1 2 0v8Z"/>
        </svg>
        <div id="alert-2" :class="alert ? 'flex items-center justify-between p-4 mb-4 text-red-800 rounded-lg bg-red-50' : 'hidden'" role="alert">
          <div class="flex items-center">
            <svg class="flex-shrink-0 w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
              <path d="M10 .5a9.5 9.5 0 1 0 9.5 9.5A9.51 9.51 0 0 0 10 .5ZM9.5 4a1.5 1.5 0 1 1 0 3 1.5 1.5 0 0 1 0-3ZM12 15H8a1 1 0 0 1 0-2h1v-3H8a1 1 0 0 1 0-2h2a1 1 0 0 1 1 1v4h1a1 1 0 0 1 0 2Z"/>
            </svg>
            <span class="sr-only">Info</span>
            <div class="ml-3 text-sm font-medium">
              <span class="font-medium">WARNING!</span> Please upload image.
            </div>
          </div>
          <button type="button" @click="alert = false" class="ml-4 -mx-1.5 -my-1.5 bg-red-50 text-red-500 rounded-lg focus:ring-2 focus:ring-red-400 p-1.5 hover:bg-red-200 inline-flex items-center justify-center h-8 w-8" data-dismiss-target="#alert-2" aria-label="Close">
            <span class="sr-only">Close</span>
            <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
            </svg>
          </button>
        </div>
        <div class="border-dashed border-2 border-sky-500 aspect-video w-full cursor-pointer flex justify-center items-center" @click="imageOpen">
          <div role="status" :class="loading ? 'absolute flex flex-col items-center' : 'hidden'">
              <svg aria-hidden="true" class="w-12 h-12 mr-2 text-gray-200 animate-spin fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/><path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/></svg>
              <span class="sr-only">Loading...</span>
              <span class="text-white text-lg">Processing...</span>
          </div>
          <img :src="imageURL" :class="imageURL === '' ? 'hidden' : 'aspect-video w-full'" alt="" srcset="" width="500" height="500">
          <h2 :class="imageURL === '' ? 'py-2 px-4 bg-gray-200 rounded-full' : 'hidden'">Select Image</h2>
        </div>
        <input type="file" id="image_input" hidden @input="imageHandle" accept="image/png, image/jpeg, image/jpg">
        <button type="button" @click="imageProcess" class="mt-6 w-full text-white lg:text-xl text-lg font-semibold bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Detect</button>
      </div>
      <div class="lg:col-span-6 col-span-12">
        <Details
            :show="showResult"
            :judul="result.judul"
            :alias="result.alias"
            :episode="result.episode"
            :awal="Math.round(result.from / 60)"
            :akhir="Math.round(result.to / 60)"
            :image="result.image"
            :clip="result.video"
        />
      </div>
    </div>
  </section>
</template>
<script>

import Navbar from './components/Navbar.vue'
import Details from './components/Details.vue'
import axios from 'axios'

export default {
  components:{
    Details,
    Navbar
  },
  data() {
    return {
      image: "",
      imageURL: "",
      imageName: "",
      result: [{
        judul: "",
        alias: ""
      }],
      alert: false,
      loading: false,
      showResult: false,
      showTrash: false
    }
  },
  methods: {
    imageOpen(){
      const imageInput = document.getElementById('image_input')
      imageInput.click()
    },
    imageHandle(){
      const imageInput = document.getElementById('image_input')
      this.image = imageInput.files[0]
      this.imageURL = URL.createObjectURL(imageInput.files[0])
      this.imageName = imageInput.files[0].name
      this.showTrash = true
    },
    removeImage(){
      this.image = ""
      this.imageURL = ""
      this.imageName = ""
      this.showTrash = false
      this.showResult = false
    },
    imageProcess(){

      if(this.image === ""){
        this.alert = true

      } else {
        
        this.loading = true
        
        const formData = new FormData()
  
        formData.append('image', this.image)
        
        axios.post('https://api.trace.moe/search?anilistInfo', formData)
  
        .then(response => {
          this.result = response.data.result[0]
          console.log(this.result)
          this.result.judul = response.data.result[0].anilist.title.english
          this.result.alias = response.data.result[0].anilist.title.romaji
          this.loading = false
          this.showResult = true
        })
  
        .catch(error => {
          console.log(error)
        })
      }
    }
  },
}
</script>
<style>
  
</style>