
<template>
  <div>
  
    <cld-image ref="ref" :public-id="publicId">
    
      <cld-transformation effect="blur:150"/>
      <cld-transformation effect="brightness_hsb:-30"/>
      <cld-transformation :overlay="{fontFamily: 'Metal Mania', fontSize: 60, fontWeight: 'bold', text: concertName, testAlign: 'center'}" color="#fff" opacity="90" crop="fit" width="550" effect="shadow"/>
      <cld-transformation flags="layer_apply"/>
      <cld-transformation :overlay="{fontFamily: 'Courgette', fontSize: 15, fontWeight: 'bold', text: `Artist: ${artist}`}" color="#fff" effect="shadow"  crop="fit" width="120" />
      <cld-transformation flags="layer_apply" gravity="south_east" x="150" y="80" />
      
    </cld-image>
    <div class="mv4">
      <label class="db mb2 f3 fw4 b">Shareable link</label>
      <input disabled type="text" class="db w-90 pv3 ph2 br2 ba b--black-40 f7" :value="url" />
      <button class="f6 link dim br2 ph3 pv2 db white bg-dark-green ba b--green mt2" @click="copyUrl">{{share}}</button>
    </div>
    
  </div>
</template>
<script>
export default {
  props: {
    concertName: { 
      type: String, 
      required: true 
    },
    artist: { 
      type: String, 
      required: true
    },
    publicId: { 
      type: String, 
      required: true
    },
  },
  data() {
    return {
      url: "",
      share: 'Share Link'
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.url = this.$refs.ref.$el.src
    });
  },
  methods: {
    copyUrl(){
      navigator.clipboard
      .writeText(this.url)
      .then(() => (this.share = 'Copied!'))
      .catch((err) => err)
    }
  },
}
</script>