<template>
  <div>
    <Gradient :eventData="event" :duration="duration"></Gradient>
    <div class="h-screen w-screen overflow-hidden">
      <div class=" w-screen z-30 left-0 fixed wrapper" style="height: 300vh;" :style="'top:'+offset+'vh'"  @wheel="changeSlide($event)">
        <div class="logo fixed top-24 left-0 z-20">
          <img src="@/assets/img/logo.svg" alt="">
        </div>
        <div class="nav fixed top-8 flex left-72 z-20">
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">works</a>
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">team</a>
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">blog</a>
          <a href="#" class="uppercase girloy text-sm text-white text-opacity-30 transition hover:text-opacity-100">contact us</a>
        </div>
        <a href="#">
          <div class="banner fixed right-32 px-6 py-8 transition duration-1000 w-72 h-20 top-0 z-20">
            <div class="w-60 h-4 relative flex items-center">
              <svg class=" absolute "  width="55" height="14" viewBox="0 0 55 14" fill="white" xmlns="http://www.w3.org/2000/svg">
                <path class="" fill-rule="evenodd" clip-rule="evenodd" d="M47.6465 1.35359L53.2929 7.00004L47.6465 12.6465L48.3536 13.3536L54.7071 7.00004L48.3536 0.646484L47.6465 1.35359ZM4 7.5H0V6.5H4V7.5ZM12 7.5H8V6.5H12V7.5ZM16 7.5H20V6.5H16V7.5ZM28 7.5H24V6.5H28V7.5ZM32 7.5H36V6.5H32V7.5ZM44 7.5H40V6.5H44V7.5Z"/>
              </svg>
              <p class="absolute right-6 uppercase text-sm girloy">LETS GET IN TOUCH</p>
            </div>
          </div>
        </a>
        <div class="scroll fixed flex top-1/2 right-1 transform rotate-90">
          <p class="girloy text-xs  uppercase opacity-30 transform rotate-180 text-white" style="height: fit-content">just scroll</p>
          <img src="./assets/img/Mouse.svg" class="w-4 transform rotate-90 mx-12"  alt="">
          <img src="./assets/img/banner_arrow.svg" class="" alt="">
        </div>
        <div class="links flex justify-between fixed bottom-24 left-72 z-20" style="width: 17.3rem;">
          <Link :link="'https://www.linkedin.com/'" :content="'In'" />
          <Link :link="'https://twitter.com/'" :content="'Tw'" />
          <Link :link="'https://medium.com/'" :content="'Md'" />
        </div>
        <div class="main-bg absolute right-96" style="width: 45.125rem;" :class="currentSlide == 0 ? 'top-32' : currentSlide == 1 ? '-top-48' : ''" :style="currentSlide == 2 ? 'top:-32rem;' : ''">
          <img src="./assets/img/main_pic.svg" alt="">
        </div>
        <div class="slide1 w-screen h-screen relative">
          <div class="anim-lines flex absolute left-5" style="top: 30.92rem">
            <div class="line h-5 border-l mr-9 opacity-30" v-for="i in 7" :key="i" :style="'animation-delay:'+0.9*i+'s ;'"></div>
          </div>
          <div class="bg absolute -right-24" style="width: 100rem; height: 100rem; top: -23rem">

          </div>
        </div>
        <div class="slide2 w-screen h-screen">
          pdfgdfg2
        </div>
        <div class="slide3 w-screen h-screen">
          pdfgdfg3
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Gradient from '@/components/Gradient/Gradient'
import Link from '@/components/Link/Link'

export default {
  name: 'App',
  components: { Gradient, Link },
  data () {
    return {
      currentSlide: 0,
      event: {},
      slides: 3,
      pastSlide: 0,
      duration: 1
    }
  },
  computed: {
    offset: function () {
      return this.currentSlide * -100
    }
  },
  methods: {
    changeSlide: function (event) {
      if (this.currentSlide === this.pastSlide) {
        this.event = event
        if (this.event.deltaY > 0 && this.currentSlide < this.slides - 1) {
          this.currentSlide++
          setTimeout(() => {
            this.pastSlide++
          }, 1000 * this.duration)
        } else if (this.event.deltaY < 0 && this.currentSlide > 0) {
          this.currentSlide--
          setTimeout(() => {
            this.pastSlide--
          }, 1000 * this.duration)
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .banner{
    background: rgba(248,64,86,1);
    svg{
      left: 0;
      transition: all linear .5s;
      path{
        fill:white;
        transition: all linear .5s;
      }
    }
    p{
      animation: 1s linear 0s 1 alternate banner;
      color: rgba(255,255,255,1);
      right: 1.5rem;
    }
  }
  .banner:hover{
    background: rgba(255,255,255,1);
    svg{
      left: 185px;
      right: 0;
      path{
        fill: rgba(248,64,86,1);
      }
    }
    p{
      color: rgba(248,64,86,1);
      animation: 1s linear 0s 1 alternate-reverse banner;
      right: auto;
      left: 0;
    }
  }
  @keyframes banner {
    0%{
      color: rgba(255,255,255,1);
      opacity: 100%;
      right: 1.5rem;
      left: auto;
    }
    10%{
      opacity: 0;
      right: 1.5rem;
      left: auto;
    }
    90%{
      left: 0;
      right: auto;
      opacity: 0;
    }
    100%{
      right: auto;
      color: rgba(248,64,86,1);
      left: 0;
      opacity: 100%;
    }
  }
  .wrapper, .main-bg {
    transition: all 1s linear;
  }
  .line{
    border-color: #A08CCB;
    animation: 6s linear infinite alternate linemove;
  }
  @keyframes linemove {
    0%, 100%{
      height: 1.25rem;
    }
    50%{
      height: 2.5rem;
    }
  }
  .bg{
    background: url("assets/img/big_circle.svg");
    background-size: cover;
    background-position: 50% 50%;

  }

</style>
