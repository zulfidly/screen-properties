<script setup>
  import { reactive } from 'vue'
  const scr = reactive({
    width: window.screen.width,
    height: window.screen.height,
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
    scr.width = window.screen.width
    scr.height = window.screen.height
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
</script>

<style scoped>
td,th {
  padding: 10px 10px;
}
</style>

<template>
  <div class="w-full h-auto grid grid-cols-1 md:grid-cols-2 gap-4 place-items-center">
    <p class="sm:hidden"> *rotate to see difference </p>
    <div class="w-full h-full border p-4 rounded-lg bg-[var(--color-background-soft)]">      
      <table class="text-center w-full h-auto text-md font-light">
        <caption class="font-bold">Width / Height</caption>
        <thead>
          <tr class="bg-[var(--color-background-mute)] [&>th]:font-semibold">
            <th>Properties</th>
            <th>W (px)</th>
            <th>H (px)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>screen.width , <br> height</td>
            <td>{{ scr.width }}</td>
            <td>{{ scr.height }}</td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>screen.availWidth , <br> availHeight</td>
            <td>{{ scr.availWidth }}</td>
            <td>{{ scr.availHeight }}</td>
          </tr>
          <tr>
            <td>screen.outerWidth , <br> outerHeight</td>
            <td>{{scr.outerWidth}}</td>
            <td>{{ scr.outerHeight }}</td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>innerWidth , <br> innerHeight</td>
            <td>{{ scr.innerWidth }}</td>
            <td>{{ scr.innerHeight }}</td>
          </tr>
          <tr>
            <td>visualViewport.width , <br> outerHeight</td>
            <td>{{scr.vv_width}}</td>
            <td>{{ scr.vv_height }}</td>
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
            <td>orientation.type</td>
            <td> {{ scr['orientation.type'] }} </td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>colorDepth</td>
            <td> {{ scr.colorDepth }} </td>
          </tr>
          <tr>
            <td>pixelDepth</td>
            <td> {{ scr.pixelDepth }} </td>
          </tr>
          <tr class="bg-[var(--color-background-mute)]">
            <td>devicePixelRatio</td>
            <td> {{ scr.devicePixelRatio }} </td>
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

