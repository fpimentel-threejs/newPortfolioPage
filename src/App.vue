<template>
  <div :data-theme='theme'>
  <!--navbar-->
    <div style="z-index: 5; position: fixed; top:0; border-width: 1px ;border-bottom: 1px dashed;" class="navbar bg-base-100">
      <div class="flex-1">
        <a v-if="theme == 'black'" @click="theme = 'lofi'; changeFill()" class="btn btn-ghost normal-case text-xl">Light Mode</a>
        <a v-if="theme == 'lofi'" @click="theme = 'black'; changeFill()" class="btn btn-ghost normal-case text-xl">Dark Mode</a>
      </div>
      <div  style="font-size: 15px" class="flex-none">
        <ul class="menu menu-horizontal px-1">
          <li><a href="#about">About</a></li>
          <li><a href="#work">My Work</a></li>
          <li><a href="#contact">Contact</a></li>
          <li><a href="/assets/fpimentel_resume.pdf">Resume</a></li>
        </ul>
      </div>
    </div>
    <div style="padding: 250px 100px;" class="">
      <div class="pb-10 text-4xl font-black">Hello, I'm Fernando.</div>
      <div class="pb-10 text-4xl font-black">I enjoy web development and 3D art.</div>
      <div class="animate-pulse place-self-center">(Scroll down to see more)</div>
    </div>
    <div id="about" class=" text-5xl p-8 ml-32">About Me</div>

    <!--canvas div 1-->
  <div style="padding: 10px 10px;  margin: 100px 0px;" id="outer">
    <div  v-show="theme=='lofi'" id="top" style=" z-index: 3;" class="flex w-full">
      <!--canvas-->
      <div style="min-width: 200px" class="mask mask-circle place-content-center">

        <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
          <Camera ref="cameraA" :position="{ z: 40 }" />
          <Scene :background="0xffffff">
            <PointLight :position="{ y: 50, z: 50 }" />

            <Points ref="starsL" :position="{x: -45, y:-40, z:-40}" :rotation="{ x: 0}"/>
            <GltfModel
                src="assets/grabMeText_light.gltf"
                @load="onReady"
                @progress="onProgress"
                @error="onError"
            />
          </Scene>
        </Renderer>
      </div>

      <div class="divider divider-horizontal"></div>

      <div style="">I am a web developer with a passion for computer graphics. Because of this I incorporate my knowledge of 3D design into the websites I create. To see what I mean, try clicking and dragging the space on the left.<br/><br/>This is a 3D canvas.</div>
    </div>

    <div v-show="theme=='black'" id="below" style="z-index: 4;" class="flex w-full">
      <!--canvas-->
      <div style="min-width: 200px" class="mask mask-circle place-content-center">

        <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
          <Camera ref="cameraA" :position="{ z: 40 }" />
          <Scene :background="0x000000">
            <PointLight :position="{ y: 50, z: 50 }" />

            <Points ref="stars" :position="{x: -45, y:-40, z:-40}" :rotation="{ x: 0}"/>
            <GltfModel
                src="assets/grabMeText.gltf"
                @load="onReady"
                @progress="onProgress"
                @error="onError"
            />
          </Scene>
        </Renderer>
      </div>

      <div class="divider divider-horizontal"></div>

      <div style="">I am a web developer with a passion for computer graphics. Because of this I incorporate my knowledge of 3D design into the websites
        I create. To see what I mean, try clicking and dragging the space on the left.<br/><br/>This is a 3D canvas.</div>
    </div>
  </div>

    <div class="p-10">I began my journey with software development at McNeese State University where I earned my bachelors of science in computer science
    with a minor in philosophy. I found my passion of 3D design and development through the senior design project I created with a partner.
    Without any specialized knowledge in this area, we created a virtual reality video game.
      <br/><br/><br/>While my skills involve 3D design and development in a variety of platforms and fields, I have most of my experience within the browser.
    Currently, I develop websites for clients both with and without 3D elements. I do this on my own terms as a freelancer, however I am now looking to fill
    a position where I can put my expertise to use with a team that shares my interests.</div>

    <div id="work" class="text-5xl mt-20 p-8 ml-20">My Work</div>

    <div class="text-3xl p-8 ml-32">AR/VR</div>

    <div>
      <div style="">My first introduction to 3D development began with VR game development.
        With a partner, we created a virtual reality video game based on a tower defense concept.
        <br/><br/>Click the video on the below to see a video demo of this game.</div>
        <br/>
      <div class="p-10 flex w-full m-8 place-content-center">
        <iframe style="height: 200px; width: 400px" src="https://www.youtube.com/embed/9WIJQ6QJ_xQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
      </div>
    </div>
    <div class="text-3xl p-8 ml-32">Web Development</div>
    <div class="p-10 flex w-full">
      <div style="">Most of the professional work I have done involves web development of some
        sort, whether it is the development of 3D web components,
         or creating small front-end sites for clients. Most notably, I've created websites
        for small businesses within e-commerce platforms for many clients,
        including <a style="color:lightblue" href="https://www.thebeautylabstl.com/">The Beauty Lab</a>, which I currently upkeep and maintain.</div>
    </div>
    <div v-show="theme=='black'" class="p-10 flex w-full">
      <div style="min-width: 200px" class="place-content-center">
        <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
          <Camera ref="cameraA" :position="{ z: 10 }" />
          <Scene>
            <PointLight :position="{ y: 50, z: 50 }" />
            <AmbientLight :position="{ y: 5, z: 2 }" :intensity=".5" />
            <GltfModel
                src="assets/PLATE_EXAMPLE.gltf"
                @load="onReady"
                @progress="onProgress"
                @error="onError"
            />
          </Scene>
        </Renderer>
      </div>
      <div class="divider divider-horizontal"></div>
      <div>
        An example of professional 3D development I've done involves a small 3D component
        for <a style="color:lightblue" href="https://www.utopiaplates.co.uk/">Utopia Plates</a>
        which involves letting the user design their own UK license plate
        within a 3D space, setting parameters for the plate's shape, border, and identifying
        markings, as well as dynamically rendering text for the plate's number.<br/><br/>
        You can see an example of one of these plates on the left.</div>
    </div>
    <div v-show="theme=='lofi'" class="p-10 flex w-full">
      <div style="min-width: 200px" class="place-content-center">
        <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
          <Camera ref="cameraA" :position="{ z: 10 }" />
          <Scene :background="0xffffff">
            <PointLight :position="{ y: 50, z: 50 }" />
            <AmbientLight :position="{ y: 5, z: 2 }" :intensity=".5" />
            <GltfModel
                src="assets/PLATE_EXAMPLE.gltf"
                @load="onReady"
                @progress="onProgress"
                @error="onError"
            />
          </Scene>
        </Renderer>
      </div>
      <div class="divider divider-horizontal"></div>
      <div>
        An example of professional 3D development I've done involves a small 3D component
        for <a style="color:lightblue" href="https://www.utopiaplates.co.uk/">Utopia Plates</a>
        which involves letting the user design their own UK license plate
        within a 3D space, setting parameters for the plate's shape, border,
        and identifying markings, as well as dynamically rendering text for the
        plate's number.<br/><br/> You can see an example of one of these plates on the left.</div>
    </div>
    <div class="p-10 flex w-full">
      <div>Other work I do involves personal passion projects like <a style="color:lightblue" href="https://polite-elf-0edf20.netlify.app/">this one</a>,
      which is a model of the solar system I am currently working on which I plan to make
      to scale. Despite how difficult it is to display scale in the context of celestial
       bodies, I believe this is easiest to accomplish in a digital 3D space.<br/><br/>
      I also spend my time creating 3D assets in blender, as you can see below.</div>
    </div>
    <div class="carousel w-full">
      <div id="slide1" class="carousel-item relative w-full">
        <img src="/assets/roserender1.png" class="w-full" />
        <div class="absolute flex justify-between transform -translate-y-1/2 left-5 right-5 top-1/2">
          <a href="#slide4" class="btn btn-circle">❮</a>
          <a href="#slide2" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide2" class="carousel-item relative w-full">
        <img src="/assets/roserender2.png" class="w-full" />
        <div class="absolute flex justify-between transform -translate-y-1/2 left-5 right-5 top-1/2">
          <a href="#slide1" class="btn btn-circle">❮</a>
          <a href="#slide3" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide3" class="carousel-item relative w-full">
        <img src="/assets/tomatocanrender.png" class="w-full" />
        <div class="absolute flex justify-between transform -translate-y-1/2 left-5 right-5 top-1/2">
          <a href="#slide2" class="btn btn-circle">❮</a>
          <a href="#slide4" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide4" class="carousel-item relative w-full">
        <img src="/assets/lastShot.png" class="w-full" />
        <div class="absolute flex justify-between transform -translate-y-1/2 left-5 right-5 top-1/2">
          <a href="#slide3" class="btn btn-circle">❮</a>
          <a href="#slide1" class="btn btn-circle">❯</a>
        </div>
      </div>
    </div>
    <div id="contact" style="height: 200px" class="text-5xl mt-20 p-8 ml-20">Contact Me</div>
    <div style="height: 200px" class="flex w-full">
      <div class="grid h-20 flex-grow place-items-center">
        <a href="https://github.com/fpimentel-threejs"><svg width="50" :fill="fillColor" version="1.2" baseProfile="tiny" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
             x="0px" y="0px" viewBox="0 0 2350 2314.8" xml:space="preserve">
          <path d="M1175,0C525.8,0,0,525.8,0,1175c0,552.2,378.9,1010.5,890.1,1139.7c-5.9-14.7-8.8-35.3-8.8-55.8v-199.8H734.4
	c-79.3,0-152.8-35.2-185.1-99.9c-38.2-70.5-44.1-179.2-141-246.8c-29.4-23.5-5.9-47,26.4-44.1c61.7,17.6,111.6,58.8,158.6,120.4
	c47,61.7,67.6,76.4,155.7,76.4c41.1,0,105.7-2.9,164.5-11.8c32.3-82.3,88.1-155.7,155.7-190.9c-393.6-47-581.6-240.9-581.6-505.3
	c0-114.6,49.9-223.3,132.2-317.3c-26.4-91.1-61.7-279.1,11.8-352.5c176.3,0,282,114.6,308.4,143.9c88.1-29.4,185.1-47,284.9-47
	c102.8,0,196.8,17.6,284.9,47c26.4-29.4,132.2-143.9,308.4-143.9c70.5,70.5,38.2,261.4,8.8,352.5c82.3,91.1,129.3,202.7,129.3,317.3
	c0,264.4-185.1,458.3-575.7,499.4c108.7,55.8,185.1,214.4,185.1,331.9V2256c0,8.8-2.9,17.6-2.9,26.4
	C2021,2123.8,2350,1689.1,2350,1175C2350,525.8,1824.2,0,1175,0L1175,0z"/>
        </svg></a>
      </div>
      <div class="grid h-20 flex-grow place-items-center">
        <a href="https://www.instagram.com/rxnando/"><svg width="50" :fill="fillColor" id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 491.4 491.4">
          <defs>
          </defs>
          <path class="cls-1" d="M452.33,.5H39.07C17.77,.5,.5,17.77,.5,39.07V452.33c0,21.3,17.27,38.57,38.57,38.57H452.33c21.3,0,38.57-17.27,38.57-38.57V39.07c0-21.3-17.27-38.57-38.57-38.57Zm-177.08,439.69c-131.71,19.18-243.22-92.34-224.04-224.04C63.61,130.98,130.98,63.61,216.15,51.21c131.71-19.18,243.22,92.34,224.04,224.04-12.4,85.17-79.77,152.54-164.94,164.94ZM430.27,92.54c-19.85,1.25-36.22-15.11-34.96-34.96,1.03-16.37,14.32-29.66,30.69-30.69,19.85-1.25,36.22,15.11,34.96,34.96-1.03,16.37-14.32,29.66-30.69,30.69Z"/>
          <circle class="cls-1" cx="245.7" cy="245.7" r="115.25"/>
        </svg></a>
      </div>
      <div class="grid h-20 flex-grow place-items-center">
        <a href="https://www.linkedin.com/in/fernando-pimentel-935143230/"><svg width="50" :fill="fillColor" id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 169.5 174.15">
          <path class="cls-1" d="M28.12,14.19c.26,7.74-5.42,13.93-14.45,13.93C5.68,28.12,0,21.93,0,14.19S5.93,0,14.19,0s13.93,6.19,13.93,14.19ZM2.84,174.15V49.28H25.54v124.87H2.84Z"/>
          <path class="cls-1" d="M63.21,83.07c0-12.9-.26-23.48-1.03-33.8h20.12l1.29,20.64h.52c6.19-11.87,20.64-23.48,41.28-23.48,17.29,0,44.12,10.32,44.12,53.15v74.56h-22.7V102.17c0-20.12-7.48-36.89-28.89-36.89-14.96,0-26.57,10.58-30.44,23.22-1.03,2.84-1.55,6.71-1.55,10.58v75.08h-22.7V83.07Z"/>
        </svg></a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { TextureLoader, BufferAttribute, BufferGeometry, PointsMaterial } from 'three'
import { AmbientLight, GltfModel, Camera, PointLight, Renderer, Scene, Points } from 'troisjs'
const rendererC = ref()
const stars = ref()
const starsL = ref()
let cameraA = ref()
const theme = ref('black')
let fillColor = ref('#ffffff')

function changeFill(){
  if(fillColor == '#000000'){
    fillColor = '#ffffff'
  }
  else{
    fillColor = '#000000'
  }
}

const material = new PointsMaterial({
  size: .3,
  color: 0xffffff
})

const materialL = new PointsMaterial({
  size: .3,
  color: 0x000000
})

const geometry = new BufferGeometry();

const getRandomParticlePos = (particleCount) => {
  const arr = new Float32Array(particleCount * 3);
  for(let i = 0; i < particleCount; i++) {
    arr[i] = (Math.random() - .05) * 100;
  }
  return arr;
}

geometry.setAttribute(
    "position",
    new BufferAttribute(getRandomParticlePos(7000),3)
);



onMounted(() => {
  const renderer = rendererC.value
  const star = stars.value
  star.setGeometry(geometry)
  star.setMaterial(material)
  const starL = starsL.value
  starL.setGeometry(geometry)
  starL.setMaterial(materialL)

  renderer.onBeforeRender(() => {

  })


})
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@300&family=Sofia+Sans+Condensed:wght@200&display=swap');

::-webkit-scrollbar {
  display: none;
}

h1{
}

body {
  font-family: 'Barlow', sans-serif;
  font-size: 20px;
}
canvas {
  width: 100%;
}

#outer {
  display: grid;
  grid-template: 1fr / 1fr;
  place-items: center;
}
#outer > * {
  grid-column: 1 / 1;
  grid-row: 1 / 1;
}
#outer .below {
  z-index: 1;
  background-color: aqua;
}
#outer .top {
  z-index: 2;
  background-color: brown;
}
</style>