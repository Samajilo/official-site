<template>
  <v-row
    align="center"
    justify="center"
    class="mb-10 ma-auto"
    height="100vh"
    style="margin-bottom: 200px!important;margin-top: 100px!important;"
  >
    <v-col cols="auto" md="6">
      <v-hover v-slot="{ hover }">
        <v-card
          :elevation="hover ? 12 : 3"
          class="pa-10 palatinoFont mt-20 animateCard"
          height="300px"
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
          <v-card-actions class="justify-center link animateThis" height="100px">
            <!-- discover our history -->
            <a href="#" class="btn-animate" width="200px" height="50px">
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
</template>

<script>
import { gsap } from "gsap/dist/gsap";
import ScrollTrigger from "gsap/dist/ScrollTrigger";

export default {
  mounted() {
    gsap.registerPlugin(ScrollTrigger);
    const content = ".animateThis";
    gsap.fromTo(
      ".animateCard",
      {
        opacity: 0,
      },
      {
        opacity: 1,
        duration: 3,
        ease: "elastic",
        y: -20,
        scrollTrigger: {
          trigger: content,
          scrub: 0.5,
        },
      }
    );
    gsap.fromTo(
      content,
      { opacity: 0 },
      {
        opacity: 1,
        duration: 3,
        y: -30,
        scrollTrigger: {
          trigger: content,
          scrub: 0.5,
        },
      }
    );

    const cursorOuter = document.querySelector(".cursor--large");
    const cursorInner = document.querySelector(".cursor--small");
    let isStuck = false;
    let mouse = {
      x: -100,
      y: -100,
    };

    let scrollHeight = 0;
    window.addEventListener("scroll", function(e) {
      scrollHeight = window.scrollY;
    });

    let cursorOuterOriginalState = {
      width: cursorOuter.getBoundingClientRect().width,
      height: cursorOuter.getBoundingClientRect().height,
    };
    const buttons = document.getElementsByClassName("animateCard")
    console.log(buttons)

    buttons.forEach((button) => {
      button.addEventListener("pointerenter", handleMouseEnter);
      button.addEventListener("pointerleave", handleMouseLeave);
    });

    document.body.addEventListener("pointermove", updateCursorPosition);
    document.body.addEventListener("pointerdown", () => {
      gsap.to(cursorInner, 0.15, {
        scale: 2,
      });
    });
    document.body.addEventListener("pointerup", () => {
      gsap.to(cursorInner, 0.15, {
        scale: 1,
      });
    });

    function updateCursorPosition(e) {
      mouse.x = e.pageX;
      mouse.y = e.pageY;
    }

    function updateCursor() {
      gsap.set(cursorInner, {
        x: mouse.x,
        y: mouse.y,
      });

      if (!isStuck) {
        gsap.to(cursorOuter, {
          duration: 0.15,
          x: mouse.x - cursorOuterOriginalState.width / 2,
          y: mouse.y - cursorOuterOriginalState.height / 2,
        });
      }

      requestAnimationFrame(updateCursor);
    }

    updateCursor();

    function handleMouseEnter(e) {
      isStuck = true;
      const targetBox = e.currentTarget.getBoundingClientRect();
      console.log(targetBox)
      gsap.to(cursorOuter, 0.2, {
        x: targetBox.left - 11,
        y: targetBox.top + scrollHeight - 10,
        width: targetBox.width,
        height: targetBox.height,
        borderRadius: 0,
        backgroundColor: "rgba(255, 255, 255, 0.1)",
      });
    }

    function handleMouseLeave(e) {
      isStuck = false;
      gsap.to(cursorOuter, 0.2, {
        width: cursorOuterOriginalState.width,
        height: cursorOuterOriginalState.width,
        borderRadius: "50%",
        backgroundColor: "transparent",
      });
    }
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
