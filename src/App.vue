<template>
  <div>
    <Gradient :eventData="event" :duration="duration"></Gradient>
    <div class="h-screen w-screen overflow-hidden">
      <div class=" w-screen z-30 left-0 fixed wrapper" style="height: 300vh;" :style="'top:'+offset+'vh'"  @wheel="changeSlide($event)">
        <div class="logo fixed top-24 left-0 z-40">
          <img src="@/assets/img/logo.svg" alt="">
        </div>
        <div class="nav fixed top-8 flex left-72 z-40">
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">works</a>
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">team</a>
          <a href="#" class="uppercase girloy text-sm mr-36 text-white text-opacity-30 transition hover:text-opacity-100">blog</a>
          <a href="#" class="uppercase girloy text-sm text-white text-opacity-30 transition hover:text-opacity-100">contact us</a>
        </div>
        <div class="banner fixed right-32 px-6 py-8 transition duration-1000 w-72 h-20 top-0 z-20 cursor-pointer" @click="showModal = true">
            <div class="w-60 h-4 relative flex items-center">
              <svg class=" absolute "  width="55" height="14" viewBox="0 0 55 14" fill="white" xmlns="http://www.w3.org/2000/svg">
                <path class="" fill-rule="evenodd" clip-rule="evenodd" d="M47.6465 1.35359L53.2929 7.00004L47.6465 12.6465L48.3536 13.3536L54.7071 7.00004L48.3536 0.646484L47.6465 1.35359ZM4 7.5H0V6.5H4V7.5ZM12 7.5H8V6.5H12V7.5ZM16 7.5H20V6.5H16V7.5ZM28 7.5H24V6.5H28V7.5ZM32 7.5H36V6.5H32V7.5ZM44 7.5H40V6.5H44V7.5Z"/>
              </svg>
              <p class="absolute right-6 uppercase text-sm girloy">LETS GET IN TOUCH</p>
            </div>
        </div>
        <div class="scroll fixed flex top-1/2 -right-12 transform rotate-90 z-20">
          <p class="girloy text-xs  uppercase opacity-30 transform rotate-180 text-white" style="height: fit-content">just scroll</p>
          <img src="./assets/img/Mouse.svg" class="w-4 transform rotate-90 mx-12"  alt="">
          <img src="./assets/img/banner_arrow.svg" class="" alt="">
        </div>
        <div class="links flex justify-between fixed bottom-20 left-72 z-40" style="width: 17.3rem;">
          <Link :link="'https://www.linkedin.com/'" :content="'In'" />
          <Link :link="'https://twitter.com/'" :content="'Tw'" />
          <Link :link="'https://medium.com/'" :content="'Md'" />
        </div>
        <div class="main-bg absolute right-96 z-20" style="width: 45.125rem;" :class="currentSlide === 0 ? 'top-32' : currentSlide === 1 ? '-top-48' : ''" :style="currentSlide === 2 ? 'top:-33rem;' : ''">
          <img src="./assets/img/main_pic.svg" alt="">
        </div>
        <div class="slide1 w-screen h-screen relative">
          <div class="anim-lines flex absolute left-5" style="top: 30.92rem">
            <div class="line h-5 border-l mr-9 opacity-30" v-for="i in 7" :key="i" :style="'animation-delay:'+0.9*i+'s ;'"></div>
          </div>
          <div class="bg absolute -right-24" style="width: 100rem; height: 100rem; top: -23rem"></div>
          <div class="link-to-2 absolute w-1/3"
               :style="currentSlide === 0 ? 'top: 38rem;' : 'top: 27.313rem;'"
               :class="currentSlide === 0 ? 'left-20' : 'left-44'">
            <img src="./assets/img/slide1/1-2.svg" alt="">
          </div>
          <div class="triangles-circles absolute left-8 top-36 w-screen" >
            <img src="./assets/img/slide1/triangles_circles.svg" alt="">
          </div>
          <div class="horizontal absolute top-44 right-72 w-32 flex">
            <img src="./assets/img/slide1/horizontal.svg" alt="">
            <div class="lines flex items-end pb-1 ml-28">
              <div class="right-line h-2 border-l ml-4" style="border-color: rgba(160,140,203,.3)" v-for="i in 10" :key="i"></div>
            </div>
          </div>
          <div class="text absolute left-72 top-64">
            <div class="header text-white  text-6xl">
              <p v-for="row in content[0].header" :key="row.id" class="py-1 overflow-hidden">
                <span v-for="(i, index) in row" :key="i.id">
                  <transition name="letters" >
                    <span v-if="pastSlide === 0" :style="currentSlide-pastSlide === 0 ? 'transition-delay:'+ 0.1 * (index+1)+'s;' : 'transition-delay: 0.5s;'" class="inline-block">
                      <pre class="prata mx-0.5">{{i}}</pre>
                    </span>
                  </transition>
                </span>
              </p>
            </div>
            <div class="content overflow-hidden mt-16">
              <transition name="content">
                <p v-if="pastSlide === 0" class="text-xl" style="color: rgba(178,163,207,0.8); width: 26rem; transition-delay: 2.2s; ">
                  {{content[0].content}}
                </p>
              </transition>

            </div>
          </div>
        </div>
        <div class="slide2 w-screen h-screen relative">
          <div class="bg-2 absolute w-screen h-screen -left-6 -top-8">
            <img src="./assets/img/slide2/ratio.svg" alt="">
          </div>
          <div class="subslide-controlers absolute left-20 top-72 flex flex-col items-center w-20" >
            <div class="border subslide-controler relative mb-12"
                 :class="subSlide[0] === subSlideIndex ? 'w-10 h-10' : 'w-3.5 h-3.5'"
                 style="border-radius: 50%; border-color: rgba(255,255,255,.5)"
                 v-for="(subslide, subSlideIndex) in content[1]" :key="subslide + subSlideIndex"
                 @click="setSubSlide(0, subSlideIndex)">
              <div class="sub-slide-marker border-t border-dashed right-1/2 absolute top-1/2"
                   :class="subSlide[0] === subSlideIndex ? 'w-8' : 'w-0'"
                   style="border-color: rgba(255,255,255,.5)"></div>
            </div>
          </div>
          <img src="./assets/img/slide2/Triangle.svg" alt="" class="triangle w-6 h-6 absolute top-44 left-80">
          <img src="./assets/img/slide2/Triangle.svg" alt="" class="triangle w-10 h-10 absolute top-40 right-36">
          <img src="./assets/img/slide2/Triangle.svg" alt="" class="triangle w-6 h-6 absolute" style="left: 41.25rem; bottom: 27rem">
          <div class="text absolute left-64 top-60">
            <div class="subslide" v-for="(subslide, subSlideIndex) in content[1]" :key="subslide.id">
              <div v-if="subSlideIndex === subSlide[0]">
                <div class="header text-white prata text-6xl">
                  <p v-for="row in subslide.header" :key="row.id" class="py-1 overflow-hidden">
                  <span v-for="(i, index) in row" :key="i.id">
                    <transition name="letters" >
                      <span v-if="pastSlide === 1 && subSlideIndex === subSlide[0]" :style="currentSlide-pastSlide === 0 ? 'transition-delay:'+ 0.1 * (index+1) +'s;' : 'transition-delay: 0.5s;'" class="inline-block">
                  <pre class="prata mx-0.5">{{i}}</pre>
                  </span>
                  </transition>
                  </span>
                  </p>
                </div>
                <div class="content overflow-hidden mt-12 mb-16">
                  <transition name="content">
                    <p v-if="pastSlide === 1 && subSlideIndex === subSlide[0]" class="text-xl" style="color: rgba(178,201,236,.8); width: 26rem; transition-delay: 1.4s">
                      {{subslide.content}}
                    </p>
                  </transition>
                </div>
                <div class="list overflow-hidden">
                  <transition name="content">
                    <div v-if="pastSlide === 1 && subSlideIndex === subSlide[0]" class="text-xl" style="color: rgba(178,201,236,.8); width: 26rem; transition-delay: 1.8s">
                      <p v-for="item in subslide.list" :key="item.id">
                        -<span class="text-white ml-10">{{item}}</span>
                      </p>

                    </div>
                  </transition>
                </div>
              </div>

            </div>
          </div>
        </div>
        <div class="slide3 w-screen h-screen relative">
          <div class="bg-3 absolute right-16 top-16">
            <img src="./assets/img/slide3/map.svg" alt="">
          </div>
          <div class="subslide-controlers absolute left-20 top-72 flex flex-col items-center w-20" >
            <div class="border subslide-controler relative mb-12"
                 :class="subSlide[1] === subSlideIndex ? 'w-10 h-10' : 'w-3.5 h-3.5'"
                 style="border-radius: 50%; border-color: rgba(255,255,255,.5)"
                 v-for="(subslide, subSlideIndex) in content[2]" :key="subslide + subSlideIndex"
                 @click="setSubSlide(1, subSlideIndex)">
              <div class="sub-slide-marker border-t border-dashed right-1/2 absolute top-1/2"
                   :class="subSlide[1] === subSlideIndex ? 'w-8' : 'w-0'"
                   style="border-color: rgba(255,255,255,.5)"></div>
            </div>
          </div>
          <div class="text absolute left-64 top-60">
            <div class="subslide" v-for="(subslide, subSlideIndex) in content[2]" :key="subslide.id">
              <div v-if="subSlideIndex === subSlide[1]">
                <div class="header text-white prata text-6xl">
                  <p v-for="row in subslide.header" :key="row.id" class="py-2 overflow-hidden">
                    <span v-for="(i, index) in row" :key="i.id">
                      <transition name="letters" >
                        <span v-if="pastSlide === 2 && subSlideIndex === subSlide[1]" :style="currentSlide-pastSlide === 0 ? 'transition-delay:'+ 0.1 * (index+1) +'s;' : 'transition-delay: 0.5s;'" class="inline-block">
                          <pre class="prata mx-0.5">{{i}}</pre>
                        </span>
                      </transition>
                    </span>
                  </p>
                </div>
                <div class="content overflow-hidden mt-12 mb-16">
                  <transition name="content">
                    <p v-if="pastSlide === 2 && subSlideIndex === subSlide[1]" class="text-xl" style="color: rgba(178,201,236,.8); width: 26rem; transition-delay: 1.8s">
                      <span v-for="item in subslide.content" class="block " :key="item.id">{{item}} <br/> <br/></span>
                    </p>
                  </transition>
                </div>
              </div>
            </div>
          </div>
        </div>
        <transition name="modal">
          <div class="modal fixed h-screen w-screen top-0 left-0 z-30 transform rotate-180"
               v-if="showModal"
               style="background: radial-gradient(69.17% 218.6% at 23.85% 23.8%, #B2C9EC 0%, #7286A3 100%);">
            <div class="relative w-screen h-screen transform rotate-180">
              <div class="scroll absolute flex top-44 -right-12 transform rotate-90 z-20 cursor-pointer transition hover:-translate-y-10" @click="showModal = false">
                <img src="./assets/img/banner_arrow.svg" class="transform rotate-180 mr-10" alt="">
                <p class="girloy text-xs  uppercase opacity-70 transform rotate-180 text-white" style="height: fit-content">BACK TO THE TOP</p>
              </div>
              <form @submit.prevent="" class="absolute left-72 top-32">
                <p class="prata text-6xl text-white">let’s get in touch</p>
                <p class="girloy text-xl mt-12 mb-7" style="color: rgba(207,219,236,1)">What are you interesting in</p>
                <div class="site-type flex">
                  <div class="relative p-8 pb-4 mr-8 w-60 h-36 flex flex-col justify-between cursor-pointer border border-white"
                       :class="modal.choosedSite !== option.name ? 'border-dashed' : ''"
                       style="border-radius: 0.75rem"
                       v-for="option in modal.siteOptions"
                       :key="option.id"
                       @click="modal.choosedSite = option.name">
                    <img :src="require('@/assets/img/modal/'+ option.icon)" alt="" class="w-6 h-6">
                    <p class="girloy text-2xl text-white " >{{option.name}}</p>

                  </div>
                </div>
                <input type="text" class="modal input border-0 border-b border-white bg-transparent block my-12 w-7/12 py-4  girloy text-white"  v-model="modal.name">
                <input type="email" class="modal input border-0 border-b border-white bg-transparent block mb-12 w-7/12 py-4 girloy text-white"  v-model="modal.email">
                <button class="transition duration-1000 flex items-center h-20 bg-white modal-send" type="submit">
                    <p class=" uppercase text-sm girloy mx-12">submit</p>
                    <svg class="mr-8"  width="55" height="14" viewBox="0 0 55 14" fill="rgba(129,150,180,1)" xmlns="http://www.w3.org/2000/svg">
                      <path class="" fill-rule="evenodd" clip-rule="evenodd" d="M47.6465 1.35359L53.2929 7.00004L47.6465 12.6465L48.3536 13.3536L54.7071 7.00004L48.3536 0.646484L47.6465 1.35359ZM4 7.5H0V6.5H4V7.5ZM12 7.5H8V6.5H12V7.5ZM16 7.5H20V6.5H16V7.5ZM28 7.5H24V6.5H28V7.5ZM32 7.5H36V6.5H32V7.5ZM44 7.5H40V6.5H44V7.5Z"/>
                    </svg>
                </button>
              </form>
              <div class="info absolute bottom-20 right-96 h-16 flex flex-col justify-center girloy text-white">
                <p>
                  email: <a href="mailto:office@wello.digital">office@wello.digital</a>
                </p>
                <p>Ukraine time: {{modal.time}}</p>
              </div>
            </div>
          </div>
        </transition>
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
      pastSlide: -1,
      duration: 1,
      subSlide: [0, 0],
      showModal: false,
      content: [
        {
          header: ['we design, develop', 'and launch digital', 'products'],
          content: 'Our clients are startup founders and company owners who have ideas to create something new. We define goals together, as partners, and find the best way to deliver a great product.'
        },
        [
          {
            header: ['branding'],
            content: 'By finding and utilizing strong points of your offer, we form a brand identity that makes your product stand out in the market',
            list: ['Naming', 'Logo design', 'Identity']
          },
          {
            header: ['design'],
            content: 'Wello way of design is the search for a solution at the junction of three areas: user needs, business efficiency, and visual aesthetics',
            list: ['UX-research', 'Rapid prototyping', 'Websites and mobile apps', 'Landing pages', 'e-Commerce']
          },
          {
            header: ['development'],
            content: 'Taking into account requirements and limitations, we determine the most appropriate technology stack and team. The development process at wello is always transparent and predictable.',
            list: ['Full-stack development', 'IOS/Android', 'Blockchain']
          },
          {
            header: ['launch'],
            content: 'Bringing the product to the market is the most exciting yet challenging stage of the project. Our focus is on building effecting strategy and making sure it goes well',
            list: ['Strategy', 'SMM-marketing', 'Market analysis']
          }
        ],
        [
          {
            header: ['interview'],
            content: ['This is a step of top significance. Our clients are experts in their business and only in close partnership can achieve high results.']
          },
          {
            header: ['prototyping'],
            content: ['We follow the lean approach for project creation.', 'Building an early prototype allows to explore ideas well and uncover bottlenecks before investing time and money into the development ']
          },
          {
            header: ['transperency &', 'predictability'],
            content: ['Repetitive progress reports that are followed with customer feedback ensure our interaction with the client along with flexible planning']
          },
          {
            header: ['support &', 'analysis'],
            content: ['The success of the project is a priority for us. We monitor and analyze projects after launch. This allows to respond to changes in a timely manner and maintain sustainable development.']
          }
        ]
      ],
      modal: {
        siteOptions: [
          {
            icon: 'Icon-1_cursor.svg',
            name: 'Web site'
          },
          {
            icon: 'Icon-2_pointer.svg',
            name: 'Mobile App'
          },
          {
            icon: 'Icon-3_parchment.svg',
            name: 'Landing page'
          },
          {
            icon: 'Icon-4_fire.svg',
            name: 'Logo & Identity'
          },
          {
            icon: 'Icon-5_purse.svg',
            name: 'Just estimate'
          }
        ],
        choosedSite: '',
        name: 'Name',
        email: 'Email',
        time: ''
      }
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
    },
    setSubSlide: function (subslide, value) {
      this.subSlide[subslide] = value
    },
    getTime: function () {
      const requestURL = 'http://worldtimeapi.org/api/timezone/Europe/Kiev.json'
      const request = new XMLHttpRequest()
      request.open('GET', requestURL)
      request.responseType = 'json'
      request.send()
      request.onload = () => {
        const fullTime = request.response
        const time = fullTime.datetime.substring(11, 16)
        let hours = parseInt(time.substring(0, 3))
        console.log(hours)
        const minutes = time.substring(2, 6)
        let postfix = 'AM'
        if (hours > 12) {
          postfix = 'PM'
          hours -= 12
          hours = '0' + hours.toString()
        }
        console.log(minutes)
        this.modal.time = hours + minutes + ' ' + postfix
      }
    }
  },
  mounted () {
    this.pastSlide = 0
    this.getTime()
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
  .wrapper, .main-bg, .link-to-2 {
    transition: all 1s linear;
  }
  .subslide-controler, .sub-slide-marker{
    transition: all .25s linear;
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
    background: url("assets/img/slide1/big_circle.svg") 50% 50%;
    background-size: cover;
  }

  .letters-enter-active {
    transition: all 0.3s linear;
  }
  .letters-enter-from {
    transform: translateY(200%);
  }
  .content-enter-active {
    transition: all 0.3s linear;
  }
  .content-enter-from {
    transform: translateY(105%);
  }
  .modal-enter-active,
  .modal-leave-active{
    transition: all 0.3s linear;
  }
  .modal-enter-from {
    left: 100%;
  }
  .modal-leave-to {
    top: -100%;
  }
  input:focus{
    outline: none;
    caret-color: white;
  }
  .modal-send{
    transition: all .25s linear;
    p{
      color: rgba(129,150,180,1)
    }
    p, svg{
      transition: all .25s linear;
    }
  }
  .modal-send:hover{
    background:rgba(129,150,180,1) ;
    p{
      color: white;
    }
    svg{
      fill: white;
    }
  }
  .choosed-site-enter-active,
  .choosed-site-leave-active {
    transition: opacity 0.25s ease;
  }

  .choosed-site-enter-from,
  .choosed-site-leave-to {
    opacity: 0;
  }

</style>
