<template>
  <div class="bg-washed-blue vh-100 ph3 ph5-ns">
    <header class="tc pv3">
      <h1 class="tl  tc tl-ns mt2 mb0 calisto fw5 f2-ns f3 mid-gray ">Custom Summer Concert Ticket Generator</h1>
    </header>
    <section class="flex flex-wrap justify-between">
      <div class="w-100 w-50-ns tc tl-ns">
        <h2 class="calisto fw1 f4-ns f3 ">Select an image</h2>

        <div v-for="ticket in tickets" :key="ticket.id" class="fl-ns db tc pa1 grow aspect-ratio--4x6 mb3" :class="ticket.id === imageId ? 'ba bw2 b--yellow ' : ''" @click="selectImage(ticket.id, ticket.publicId)">
          <cld-image :public-id="ticket.publicId" crop="scale" width="130" height="100"></cld-image>
        </div>

        <p v-if="formData.error" class="cb red fw3 i f7">Please fill the required fields</p>
        
        <div class="mv4 cb">
        
          <div class="mb3">
            <label class="mb1 ttc f7 db b" for="concert-name">Concert Name</label>
            <input id="concert-name" v-model="formData.concertName" type="text" name="concert-name" class="db w-80-l w-90-m w-100 pv3 ph2 br2 ba b--black-40 f7 bg-washed-blue" required>
          </div>

          <div class="mb3">
            <label class="mb1 ttc f7 db b" for="artist">Artist</label>
            <input id="artist" v-model="formData.artist" type="text" name="artist" class="db w-80-l w-90-m w-100 pv3 ph2 br2 ba b--black-40 f7 bg-washed-blue" required>
          </div>

        </div>
        
        <button class="f6 link dim br2 ph3 pv2 mb2 dib white bg-navy ba b--navy pointer" @click="handleSubmit">Generate Ticket</button>
        
      </div>
       <div class="w-100 w-50-ns pa3">
        <h2 class="calisto fw1 f4-ns f3 underline">Result</h2>
        <div v-if="showConcertTicket" class="mt-10">
          <GeneratedConcertTicket
            :concertName="formData.concertName"
            :artist="formData.artist"
            :publicId="formData.publicId"
          />
        </div>
      </div>
    </section>
  </div>
</template>
<script>
  import tickets from "~/utils/ticket.json";
  export default {
    data() {
      return {
        tickets,
        imageId: null,
        showConcertTicket: false,
        formData: {
          publicId: null,
          error: false,          
          concertName: '',
          artist: '',
        }
      }
    },
  methods: {
    selectImage(imageId, publicId) {
      this.imageId = imageId
      this.formData.publicId = publicId
      this.formData.error = false
      this.showConcertTicket = false
    },
    handleSubmit() {
      if (!this.imageId || (this.formData.concertName === ''|| this.formData.artist === '')) {
        this.formData.error = true
      } else {
        this.showConcertTicket = true 
      }
    },
  }
}
</script>