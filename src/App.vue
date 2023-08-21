<script setup>
  import { reactive } from 'vue'
  import { computed } from 'vue'

  const scr = reactive({
    width: window.screen.width,
    height: window.screen.height,
    WHratio: window.screen.width/window.screen.height,
    availWidth: window.screen.availWidth,
    availHeight: window.screen.availHeight,
    innerWidth: window.innerWidth,
    innerHeight: window.innerHeight,
    outerWidth: window.outerWidth,
    outerHeight: window.outerHeight,
    vv_width: visualViewport.width.toFixed(0),
    vv_height: visualViewport.height.toFixed(0),
    vv_scale: visualViewport.scale.toFixed(2),
    'orientation.type': window.screen.orientation.type,
    colorDepth: window.screen.colorDepth,
    pixelDepth: window.screen.pixelDepth,
    devicePixelRatio: window.devicePixelRatio.toFixed(4),
  })

  window.addEventListener('resize', ()=> {
    console.log("window.addEventListener('resize', ()=> {})");
    scr.width = window.screen.width
    scr.height = window.screen.height
    scr.WHratio = window.screen.width/window.screen.height
    scr.availWidth = window.screen.availWidth
    scr.availHeight = window.screen.availHeight
    scr.innerWidth = window.innerWidth
    scr.innerHeight = window.innerHeight
    scr.outerWidth = window.outerWidth
    scr.outerHeight = window.outerHeight
    scr['orientation.type'] = window.screen.orientation.type
    scr.colorDepth = window.screen.colorDepth
    scr.pixelDepth = window.screen.pixelDepth
    scr.devicePixelRatio = window.devicePixelRatio.toFixed(4)
    scr.vv_width = visualViewport.width.toFixed(0)
    scr.vv_height = visualViewport.height.toFixed(0)
    scr.vv_scale = visualViewport.scale.toFixed(2)
  })
  const W_hardwareResolution = computed(()=> {  return (scr.width * devicePixelRatio).toFixed(2) })
  const H_hardwareResolution = computed(()=> {  return (scr.height * devicePixelRatio).toFixed(2) })

  const formFactor = computed(()=> {
    if(scr['orientation.type']=='portrait-primary' || scr['orientation.type']=='portrait-secondary') {
      let ratio = window.screen.width / window.screen.height
      if(window.screen.height < 1024) {     // entering hand-held devices
        if      (ratio < 0.5) return 'Smartphone'
        else if (0.5 <= ratio && ratio < 1) return 'Tablet'
        else return 'unknown1'
      }
      else {    // if height > 1024px in portrait i.e: vertical LED screen
        return 'Desktop|Laptop'
      }
    }
    else if(scr['orientation.type']=='landscape-primary' || scr['orientation.type']=='landscape-secondary') {
      if(window.screen.width < 1024) {
        let ratio = window.screen.height / window.screen.width
        if      (ratio < 0.5) return 'Smartphone'
        else if (0.5 <= ratio && ratio < 1) return 'Tablet'
        else return 'unknown2'
      }
      else {    // if width > 1024px in landscape i.e: laptops or normal horizontal desktop screens 
        return 'Desktop|Laptop'
      }
    }
    else return 'unknown3'
  })
</script>

<style scoped>
td,th {
  padding: 10px 10px;
}
</style>

<template>
  <div class="p-2 w-full h-auto grid grid-cols-1 md:grid-cols-2 gap-4 place-items-start">
    <p class="sm:hidden"> *rotate to see difference</p>
    <div class="w-full h-full border p-4 rounded-lg bg-[var(--color-background-soft)]">      
      <table class="text-center w-full h-auto text-md font-light">
        <caption class="font-bold">Width | Height (CSS perspective)</caption>
        <thead>
          <tr class="bg-[var(--color-background-mute)] [&>th]:font-semibold">
            <th>Properties</th>
            <th>W (px)</th>
            <th>H (px)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>screen.width, <br> height</td>
            <td>{{ scr.width }}</td>
            <td>{{ scr.height }}</td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>screen.availWidth, <br> availHeight</td>
            <td>{{ scr.availWidth }}</td>
            <td>{{ scr.availHeight }}</td>
          </tr>
          <tr>
            <td>screen.outerWidth, <br> outerHeight</td>
            <td>{{scr.outerWidth}}</td>
            <td>{{ scr.outerHeight }}</td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>innerWidth, <br> innerHeight</td>
            <td>{{ scr.innerWidth }}</td>
            <td>{{ scr.innerHeight }}</td>
          </tr>
          <tr>
            <td>visualViewport.width, <br> visualViewport.height</td>
            <td>{{scr.vv_width}}</td>
            <td>{{ scr.vv_height }}</td>
          </tr>
        </tbody>
      </table> 
    </div>

    <div class="w-full h-auto border p-4 rounded-lg bg-[var(--color-background-soft)]">      
      <table class="table text-center w-full h-auto text-md font-light">
        <caption class="font-bold">Width | Height (hardware perspective)</caption>
        <thead>
          <tr class="bg-[var(--color-background-mute)] [&>th]:font-semibold">
            <th>Resolution</th>
            <th>W (px)</th>
            <th>H (px)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>
              screen.width &#215; devicePixelRatio, <br> 
              screen.height &#215; devicePixelRatio
            </td>
            <td>{{ W_hardwareResolution }}</td>
            <td>{{ H_hardwareResolution }}</td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>Form factor</td>
            <td colspan="2">{{ formFactor }}</td>
          </tr>
          <tr>
            <td>orientation.type</td>
            <td colspan="2"> {{ scr['orientation.type'] }} </td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>devicePixelRatio</td>
            <td colspan="2"> {{ scr.devicePixelRatio }} </td>
          </tr>

        </tbody>
      </table> 
    </div>


    <div class="w-full h-full border p-4 rounded-lg bg-[var(--color-background-soft)]">
      <table class="h-auto text-center w-full text-md font-light">
        <caption class="font-bold">Other Properties</caption>
        <thead>
          <tr class="bg-[var(--color-background-mute)] [&>th]:font-semibold">
            <th>Properties</th>
            <th>Data (in pixels)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>pixelDepth</td>
            <td> {{ scr.pixelDepth }} </td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>colorDepth</td>
            <td> {{ scr.colorDepth }} </td>
          </tr>
          <tr>
            <td>visualViewport.scale</td>
            <td> {{ scr.pixelDepth }} </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

