<template>
<div>
  <v-row
    align="center"
    justify="center"
    class="mb-10 ma-auto"
    style="margin-bottom: 200px!important;margin-top: 100px!important;"
  >
    <v-col cols="auto" md="6">
      <v-hover v-slot="{ hover }">
        <v-card
          :elevation="hover ? 12 : 3"
          class="pa-10 palatinoFont mt-20 animateCard stopHere thisCardToPin"
        >
          <v-card-title class="title animateThis">
            We create 360<sup>o</sup> &nbsp; value by embrasing change.
          </v-card-title>
          <v-card-text>
            <div class="description animateThis">
              We now work with 91 of the Fortune Global 100. As of 2020, we've
              made 18 consecutive appearances on the list of Fortune's "World's
              Most Admired Companies". And that's just the beginning.
            </div>
          </v-card-text>
          <v-card-actions class="justify-center link animateThis">
            <!-- discover our history -->
            <a href="#" class="btn-animate">
              <svg>
                <rect class="shape" height="50" width="200" />
              </svg>
              <span>discover our history</span>
            </a>
          </v-card-actions>
        </v-card>
      </v-hover>
    </v-col>
    <div class="cursor cursor--large"></div>
    <div class="cursor cursor--small"></div>
  </v-row>
  <v-row>
    <VintageWithText />
  </v-row>
  </div>
</template>

<script>
import { gsap } from "gsap/dist/gsap";
import ScrollTrigger from "gsap/dist/ScrollTrigger";
import VintageWithText from "../components/VintageWithText";

export default {
  data() {
    return {
      mouse: {
        x: -100,
        y: -100,
      },
      isStuck: false,
      cursorOuter: "",
      cursorInner: "",
      scrollHeight: 0,
      cursorOuterOriginalState: {},
    };
  },
  components: {
    VintageWithText
  },
  mounted() {
    // Define the cursor
    this.cursorOuter = document.querySelector(".cursor--large");
    this.cursorInner = document.querySelector(".cursor--small");
    this.cursorOuterOriginalState = {
      width: this.cursorOuter.getBoundingClientRect().width,
      height: this.cursorOuter.getBoundingClientRect().height,
    };

    // Register the plugins
    gsap.registerPlugin(ScrollTrigger);

    // Scroll Trigger animation
    const content = ".animateThis";
    const cardPin = ".thisCardToPin"
    gsap.fromTo( cardPin,
      {opacity: 0},
    {
      opacity: 1,
      duration: 1,
        scrollTrigger: {
          trigger: cardPin,
          start: "top center",
          end: "+=300",
          pin: true,
          toggleActions: "play restart restart none",
          scrub: 1,
          markers: true,
        },
      }
    );

    // add event listeners for mouse movement
    window.addEventListener("scroll", function(e) {
      this.scrollHeight = window.scrollY;
    });
    const stopCursor = document.getElementsByClassName("stopHere");
    stopCursor.forEach((stopCursor) => {
      stopCursor.addEventListener("pointerenter", this.handleMouseEnter);
      stopCursor.addEventListener("pointerleave", this.handleMouseLeave);
    });
    document.body.addEventListener("pointermove", this.updateCursorPosition);
    document.body.addEventListener("pointerdown", () => {
      gsap.to(this.cursorInner, 0.15, {
        scale: 2,
      });
    });
    document.body.addEventListener("pointerup", () => {
      gsap.to(this.cursorInner, 0.15, {
        scale: 1,
      });
    });
    this.updateCursor();
  },
  methods: {
    updateCursorPosition(e) {
      const wm = this;
      wm.mouse.x = e.pageX;
      wm.mouse.y = e.pageY;
    },
    updateCursor() {
      gsap.set(this.cursorInner, {
        x: this.mouse.x,
        y: this.mouse.y,
      });

      if (!this.isStuck) {
        gsap.to(this.cursorOuter, {
          duration: 0.15,
          x: this.mouse.x - this.cursorOuterOriginalState.width / 2,
          y: this.mouse.y - this.cursorOuterOriginalState.height / 2,
        });
      }

      requestAnimationFrame(this.updateCursor);
    },
    handleMouseEnter(e) {
      this.isStuck = true;
      const targetBox = e.originalTarget.getBoundingClientRect();
      gsap.to(this.cursorOuter, 0.2, {
        x: targetBox.left - 11,
        y: targetBox.top + scrollHeight - 10,
        width: targetBox.width,
        height: targetBox.height,
        borderRadius: 0,
        backgroundColor: "rgba(255, 255, 255, 0.1)",
      });
    },
    handleMouseLeave(e) {
      this.isStuck = false;
      gsap.to(this.cursorOuter, 0.2, {
        width: this.cursorOuterOriginalState.width,
        height: this.cursorOuterOriginalState.width,
        borderRadius: "50%",
        backgroundColor: "transparent",
      });
    },
  },
};
</script>

<style scoped>
.title {
  font-size: 1.75rem !important;
}
.description {
  font-family: "Palatino Linotype", sans-serif;
  font-size: 1.5rem !important;
}
.link {
  font-size: 1.3rem !important;
}
</style>
<style lang="scss" scoped>
$primary: #1976d2;
$filling_primary: #358ade;
$fs: "Lato", sans-serif;
$base: #000000;
$bg: #1976d2;
$w: 200px;
$h: 50px;
$blue: #19b5fe;

.cursor {
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  position: absolute;
  left: 0;
  top: 0;
  pointer-events: none;
  z-index: 100;
  &--large {
    --size: 40px;
    border: 1px solid rgb(57, 73, 171);
  }
  &--small {
    --size: 10px;
    background: rgb(255, 60, 60);
    transform: translate(-50%, -50%);
  }
}

p {
  font-family: $fs;
  color: darken($base, 30%);
}
.btn-animate {
  text-decoration: none;
  font-family: $fs;
  color: #fff;
  position: relative;
  display: inline-block;
  margin: 0 auto;
  width: $w;
  height: $h;
  overflow: hidden;
  > svg {
    position: absolute;
    top: 0;
    left: 0;
    width: $w;
    height: $h;
    stroke-width: 8px;
    stroke: $base;
    stroke-linecap: round;
    fill: transparent;
  }
  > span {
    color: $base;
    width: $w;
    height: $h;
    display: inline-block;
    text-align: center;
    font-size: 20px;
    position: absolute;
    left: 0;
    top: 0;
    line-height: 2.3;
    transition: all 0.2s ease;
    &:after {
      position: absolute;
      content: "Let's GO!";
      color: white !important;
      top: 0;
      left: -100%;
      width: $w;
      height: $h;
      color: $bg;
      transition: all 0.2s ease;
    }
    &:before {
      position: absolute;
      content: "";
      height: $h;
      z-index: 0;
      width: $h;
      background-color: $base;
      border-radius: 50%;
      top: 0;
      left: -63%;
      transition: all 0.4s ease;
      transform: scale(0);
      opacity: 0;
    }
  }
  &:hover > svg {
    transition-delay: 250ms;
    background-color: fade(black, 40%);
    color: white;
    animation: 1s pencil linear forwards;
  }
  &:hover > span {
    left: 100%;
  }
  &:hover > span:after {
    left: -100%;
  }
}
@keyframes pencil {
  0% {
    stroke-dasharray: 300;
    stroke-dashoffset: 700;
    stroke-width: 8px;
  }
  75% {
    stroke-dasharray: 900;
    stroke-dashoffset: 400;
    stroke-width: 1px;
    fill: $filling_primary;
  }
  100% {
    stroke-dasharray: 900;
    stroke-dashoffset: 400;
    stroke-width: 1px;
    fill: $primary;
  }
}
</style>
