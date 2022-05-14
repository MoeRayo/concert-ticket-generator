
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
}
</script>