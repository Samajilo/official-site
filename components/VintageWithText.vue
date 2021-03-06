<template>
  <v-row height="100vh">
    <main role="main" class="main-content" id="main-content" height="100vh">
      <div class="titleCont">
        <h1 class="main-title" id="main-title">
          "Here, in the forest,<br />
          <span
            style="padding-left:100px"
          >
            dark and deep,
          </span>
          <br />
          <span
            style="padding-right:110px"
          >
            I offer you,
          </span>
          <br />
          <span
            style="padding-left:-20px"
          >
            eternal sleep."
          </span>
        </h1>
      </div>
      <canvas id="noise" class="noise"></canvas>
      <div class="vignette"></div>
    </main>
  </v-row>
</template>

<script>
import { gsap } from 'gsap/dist/gsap'
import { TweenMax, TimelineMax } from 'gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'

export default {

  mounted () {

    gsap.registerPlugin(TweenMax, TimelineMax, ScrollTrigger)
    gsap.fromTo( ".main-content",
      {opacity: 1},
    {
      opacity: 0,
      duration: 1,
        scrollTrigger: {
          trigger: ".main-content",
          start: "bottom center",
          end: "+=300",
          toggleActions: "play restart restart none",
          scrub: 1,
          markers: true,
        },
      },
      )
    var title = document.getElementById('main-title').cloneNode(true)
    document.querySelector('.titleCont').appendChild(title)
    title.classList.add("overTitle")
    var line = document.createElement('div')
    line.className = 'line'
    document.getElementById('main-content').appendChild(line)
    var tl = new TimelineMax({repeat:-1})

    for(var i=50; i--;){
      tl.to(title,R(0.03,0.17),{opacity:R(0,1),y:R(-1.5,1.5), x:R(-1.5,1.5)})
    }
    tl.to(line,tl.duration()/2,{opacity:R(0.1,1),x:R(-window.innerWidth/2,window.innerWidth/2),ease:"rough({strength:0.5,points:10,randomize:true,taper: 'none'})", repeat:1},0)
    var dot
    for (var i=0; i < 10; i++){
      dot = document.createElement('div')
      dot.className = 'dot'
      document.getElementById('main-content').prepend(dot)
     setDotPosition(dot)
      tl.to(dot,0.1,{opacity:0,repeat:1, yoyo:true, onComplete:setDotPosition, onCompleteParams:[dot], ease:"rough({strength:0.5,points:10,randomize:true,taper: 'none'})"},0)
    }

    function setDotPosition(dot) {
      TweenMax.set(dot, {x:R(-window.innerWidth/2,window.innerWidth/2),y:R(-window.innerHeight,window.innerHeight), delay:R(0, 1)})
    }

    function R(max,min){ return Math.random()*(max-min)+min }
    const noise = () => {
      let canvas, ctx
      let wWidth, wHeight
      const noiseData = []
      let frame = 0
      let loopTimeout
      const createNoise = () => {
        const idata = ctx.createImageData(wWidth, wHeight)
        const buffer32 = new Uint32Array(idata.data.buffer)
        const len = buffer32.length
        for (let i = 0; i < len; i++) {
          if (Math.random() < 0.5) {
            buffer32[i] = 0xff000000
          }
        }
        noiseData.push(idata)
      }
      const paintNoise = () => {
        if (frame === 9) {
          frame = 0
        } else {
          frame++
        }
        ctx.putImageData(noiseData[frame], 0, 0)
      }
      const loop = () => {
        paintNoise(frame)
        loopTimeout = window.setTimeout(() => {
          window.requestAnimationFrame(loop)
        }, 1000 / 25)
      }

      const setup = () => {
        wWidth = window.innerWidth
        wHeight = window.innerHeight
        canvas.width = wWidth
        canvas.height = wHeight

        for (let i = 0; i < 10; i++) {
          createNoise()
        }
        loop()
      }
      let resizeThrottle
      const reset = () => {
        window.addEventListener(
          'resize',
          () => {
            window.clearTimeout(resizeThrottle)

            resizeThrottle = window.setTimeout(() => {
              window.clearTimeout(loopTimeout)
              setup()
            }, 200)
          },
          false
        )
      }
      // Init
      const init = (() => {
        canvas = document.getElementById('noise')
        ctx = canvas.getContext('2d')
        setup()
      })()
    }
    noise()
  }
}
</script>

<style>
.main-content {
  overflow: hidden;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column;
  height: 100vh;
  background: linear-gradient(
    to right,
    rgba(36, 31, 31, 1) 0%,
    rgba(36, 31, 31, 1) 32%,
    rgba(74, 71, 70, 1) 100%
  );
  color: #fff;
  text-align: center;
  width: 100vw;
}

.vignette {
  position: absolute;
  width: 100%;
  height: 100%;
  box-shadow: inset 0px 0px 150px 20px black;
  mix-blend-mode: multiply;
  -webkit-animation: vignette-anim 3s infinite; /* Safari 4+ */
  -moz-animation: vignette-anim 3s infinite; /* Fx 5+ */
  -o-animation: vignette-anim 3s infinite; /* Opera 12+ */
  animation: vignette-anim 3s infinite; /* IE 10+, Fx 29+ */
}

.noise {
  z-index: 100;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  opacity: 0.15;
}

.line {
  position: absolute;
  height: 100%;
  width: 1px;
  opacity: 0.1;
  background-color: #000;
}
.titleCont {
  position: relative;
}
.main-title {
  padding: 0.3em 1em 0.25em;
  font-weight: 400;
  font-size: 40px;
  color: white;
  font-family: "Bellefair", serif;
  position: relative;
  line-height: 1.3;
  /* white-spacing: */
}

.overTitle {
  position: absolute;
  top: 0;
  left: 0;
}

.dot {
  width: 3px;
  height: 2px;
  background-color: white;
  position: absolute;
  opacity: 0.3;
}
@-webkit-keyframes vignette-anim {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}
@-moz-keyframes vignette-anim {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}
@-o-keyframes vignette-anim {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}
@keyframes vignette-anim {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}
</style>
