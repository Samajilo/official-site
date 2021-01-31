<template>
  <v-row
    align="center"
    justify="center"
    height="100vh"
    style="margin-top:500px; margin-bottom: 500px;"
  >
    <v-col cols="12">
      <div class="app">
        <div class="cardList">
          <button class="cardList__btn btn btn--left">
            <div class="icon">
              <svg>
                <use xlink:href="#arrow-left"></use>
              </svg>
            </div>
          </button>
          <div
            class="cards__wrapper"
            style="height: 350px!important; width:250px!important;"
          >
            <div class="card current--card">
              <div class="card__image">
                <img src="../static/slider/prince.jpg" alt="" />
              </div>
            </div>
            <div class="card next--card">
              <div class="card__image">
                <img src="../static/slider/leo2.jpg" alt="" />
              </div>
            </div>

            <div class="card previous--card">
              <div class="card__image">
                <img src="../static/slider/merin.jpg" alt="" />
              </div>
            </div>
          </div>

          <button class="cardList__btn btn btn--right">
            <div class="icon">
              <svg>
                <use xlink:href="#arrow-right"></use>
              </svg>
            </div>
          </button>
        </div>

        <div class="infowalaList" color="transparent">
          <div class="infowala__wrapper">
            <div class="infowala current--infowala">
              <h1 class="text name">Prince Shrestha</h1>
              <h4 class="text location">CEO</h4>
              <p class="text description">
                "Samajilo is the only one thing <br />
                that will solve all your problems"
              </p>
              <div style="color: white;" class="infowalaLink">
                Link Here
              </div>
            </div>
            <div class="infowala next--infowala">
              <h1 class="text name">Mausam Dahal</h1>
              <h4 class="text location">Security Analyst<br/> & FUll-Stack Developer</h4>
              <p class="text description">
                Experience needs the courage to move from where you are.
              </p>
            </div>
            <div class="infowala previous--infowala">
              <h1 class="text name">Merin Baskota</h1>
              <h4 class="text location">Full-Stack Developer</h4>
              <p class="text description">
                I experienced working with Samajilo team <br/> and It's the best team I have ever worked for.
              </p>
            </div>
          </div>
        </div>

        <div class="app__bg">
          <div class="app__bg__image current--image">
            <img src="https://source.unsplash.com/Z8dtTatMVMw" alt="" />
          </div>
          <div class="app__bg__image next--image">
            <img src="https://source.unsplash.com/9dmycbFE7mQ" alt="" />
          </div>
          <div class="app__bg__image previous--image">
            <img src="https://source.unsplash.com/m7K4KzL5aQ8" alt="" />
          </div>
        </div>
      </div>

      <svg class="icons" style="display: none;">
        <symbol
          id="arrow-left"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 512 512"
        >
          <polyline
            points="328 112 184 256 328 400"
            style="fill:none;stroke:#fff;stroke-linecap:round;stroke-linejoin:round;stroke-width:48px"
          />
        </symbol>
        <symbol
          id="arrow-right"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 512 512"
        >
          <polyline
            points="184 112 328 256 184 400"
            style="fill:none;stroke:#fff;stroke-linecap:round;stroke-linejoin:round;stroke-width:48px"
          />
        </symbol>
      </svg>
    </v-col>
  </v-row>
</template>
<script>
import { gsap } from "gsap/dist/gsap";
import imagesLoaded from "../assets/external/imagesloaded.pkgd.min.js";
export default {
  mounted() {
    // const { gsap, imagesLoaded } = window;

    const buttons = {
      prev: document.querySelector(".btn--left"),
      next: document.querySelector(".btn--right"),
    };
    const cardsContainerEl = document.querySelector(".cards__wrapper");
    const appBgContainerEl = document.querySelector(".app__bg");

    const cardInfosContainerEl = document.querySelector(".infowala__wrapper");

    buttons.next.addEventListener("click", () => swapCards("right"));

    buttons.prev.addEventListener("click", () => swapCards("left"));

    function swapCards(direction) {
      const currentCardEl = cardsContainerEl.querySelector(".current--card");
      const previousCardEl = cardsContainerEl.querySelector(".previous--card");
      const nextCardEl = cardsContainerEl.querySelector(".next--card");

      const currentBgImageEl = appBgContainerEl.querySelector(
        ".current--image"
      );
      const previousBgImageEl = appBgContainerEl.querySelector(
        ".previous--image"
      );
      const nextBgImageEl = appBgContainerEl.querySelector(".next--image");

      changeInfo(direction);
      swapCardsClass();

      removeCardEvents(currentCardEl);

      function swapCardsClass() {
        currentCardEl.classList.remove("current--card");
        previousCardEl.classList.remove("previous--card");
        nextCardEl.classList.remove("next--card");

        currentBgImageEl.classList.remove("current--image");
        previousBgImageEl.classList.remove("previous--image");
        nextBgImageEl.classList.remove("next--image");

        currentCardEl.style.zIndex = "50";
        currentBgImageEl.style.zIndex = "-2";

        if (direction === "right") {
          previousCardEl.style.zIndex = "20";
          nextCardEl.style.zIndex = "30";

          nextBgImageEl.style.zIndex = "-1";

          currentCardEl.classList.add("previous--card");
          previousCardEl.classList.add("next--card");
          nextCardEl.classList.add("current--card");

          currentBgImageEl.classList.add("previous--image");
          previousBgImageEl.classList.add("next--image");
          nextBgImageEl.classList.add("current--image");
        } else if (direction === "left") {
          previousCardEl.style.zIndex = "30";
          nextCardEl.style.zIndex = "20";

          previousBgImageEl.style.zIndex = "-1";

          currentCardEl.classList.add("next--card");
          previousCardEl.classList.add("current--card");
          nextCardEl.classList.add("previous--card");

          currentBgImageEl.classList.add("next--image");
          previousBgImageEl.classList.add("current--image");
          nextBgImageEl.classList.add("previous--image");
        }
      }
    }

    function changeInfo(direction) {
      let currentInfoEl = cardInfosContainerEl.querySelector(".current--infowala");
      let previousInfoEl = cardInfosContainerEl.querySelector(
        ".previous--infowala"
      );
      let nextInfoEl = cardInfosContainerEl.querySelector(".next--infowala");

      gsap
        .timeline()
        .to([buttons.prev, buttons.next], {
          duration: 0.2,
          opacity: 0.5,
          pointerEvents: "none",
        })
        .to(
          currentInfoEl.querySelectorAll(".text"),
          {
            duration: 0.4,
            stagger: 0.1,
            translateY: "-120px",
            opacity: 0,
          },
          "-="
        )
        .call(() => {
          swapInfosClass(direction);
        })
        .call(() => initCardEvents())
        .fromTo(
          direction === "right"
            ? nextInfoEl.querySelectorAll(".text")
            : previousInfoEl.querySelectorAll(".text"),
          {
            opacity: 0,
            translateY: "40px",
          },
          {
            duration: 0.4,
            stagger: 0.1,
            translateY: "0px",
            opacity: 1,
          }
        )
        .to([buttons.prev, buttons.next], {
          duration: 0.2,
          opacity: 1,
          pointerEvents: "all",
        });

      function swapInfosClass() {
        currentInfoEl.classList.remove("current--infowala");
        previousInfoEl.classList.remove("previous--infowala");
        nextInfoEl.classList.remove("next--infowala");

        if (direction === "right") {
          currentInfoEl.classList.add("previous--infowala");
          nextInfoEl.classList.add("current--infowala");
          previousInfoEl.classList.add("next--infowala");
        } else if (direction === "left") {
          currentInfoEl.classList.add("next--infowala");
          nextInfoEl.classList.add("previous--infowala");
          previousInfoEl.classList.add("current--infowala");
        }
      }
    }

    function updateCard(e) {
      const card = e.currentTarget;
      const box = card.getBoundingClientRect();
      const centerPosition = {
        x: box.left + box.width / 2,
        y: box.top + box.height / 2,
      };
      let angle = Math.atan2(e.pageX - centerPosition.x, 0) * (35 / Math.PI);
      gsap.set(card, {
        "--current-card-rotation-offset": `${angle}deg`,
      });
      const currentInfoEl = cardInfosContainerEl.querySelector(
        ".current--infowala"
      );
      gsap.set(currentInfoEl, {
        rotateY: `${angle}deg`,
      });
    }

    function resetCardTransforms(e) {
      const card = e.currentTarget;
      const currentInfoEl = cardInfosContainerEl.querySelector(
        ".current--infowala"
      );
      gsap.set(card, {
        "--current-card-rotation-offset": 0,
      });
      gsap.set(currentInfoEl, {
        rotateY: 0,
      });
    }

    function initCardEvents() {
      const currentCardEl = cardsContainerEl.querySelector(".current--card");
      currentCardEl.addEventListener("pointermove", updateCard);
      currentCardEl.addEventListener("pointerout", (e) => {
        resetCardTransforms(e);
      });
    }

    initCardEvents();

    function removeCardEvents(card) {
      card.removeEventListener("pointermove", updateCard);
    }

    function init() {
      let tl = gsap.timeline();

      tl.to(cardsContainerEl.children, {
        delay: 0.15,
        duration: 0.5,
        stagger: {
          ease: "power4.inOut",
          from: "right",
          amount: 0.1,
        },
        "--card-translateY-offset": "0%",
      })
        .to(
          cardInfosContainerEl
            .querySelector(".current--infowala")
            .querySelectorAll(".text"),
          {
            delay: 0.5,
            duration: 0.4,
            stagger: 0.1,
            opacity: 1,
            translateY: 0,
          }
        )
        .to(
          [buttons.prev, buttons.next],
          {
            duration: 0.4,
            opacity: 1,
            pointerEvents: "all",
          },
          "-=0.4"
        );
    }

    const waitForImages = () => {
      const images = [...document.querySelectorAll("img")];
      const totalImages = images.length;
      let loadedImages = 0;
      const loaderEl = document.querySelector(".loader span");

      gsap.set(cardsContainerEl.children, {
        "--card-translateY-offset": "100vh",
      });
      gsap.set(
        cardInfosContainerEl
          .querySelector(".current--infowala")
          .querySelectorAll(".text"),
        {
          translateY: "40px",
          opacity: 0,
        }
      );
      gsap.set([buttons.prev, buttons.next], {
        pointerEvents: "none",
        opacity: "0",
      });

      images.forEach((image) => {
        imagesLoaded(image, (instance) => {
          if (instance.isComplete) {
            loadedImages++;
            let loadProgress = loadedImages / totalImages;

            gsap.to(loaderEl, {
              duration: 1,
              scaleX: loadProgress,
              backgroundColor: `hsl(${loadProgress * 120}, 100%, 50%`,
            });

            if (totalImages == loadedImages) {
              init();
            }
          }
        });
      });
    };

    waitForImages();
  },
};
</script>
<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@500;600;700;800&display=swap");
$cardWidth: 600px;
$card-width: 200px;
$card-height: 300px;
$card-transition-duration: 800ms;
$card-transition-easing: ease;
:root {
	--card-width: 200px;
	--card-height: 300px;

	--card-transition-duration: 800ms;
	--card-transition-easing: ease;
}
.card {
	--card-width: 600px;
	--card-height: 400px;

	--card-transition-duration: 800ms;
	--card-transition-easing: ease;
}


button {
	border: none;
	background: none;
	cursor: pointer;
	&:focus {
		outline: none;
		border: none;
	}
}

.app {
	position: relative;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: center;
	align-items: center;

	&__bg {
		position: absolute;
		width: 100%;
		height: 100%;
		z-index: -5;
		filter: blur(8px);
		pointer-events: none;
		user-select: none;
		overflow: hidden;

		&::before {
			content: "";
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			background: #000;
			z-index: 1;
			opacity: 0.8;
		}

		&__image {
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, -50%) translateX(var(--image-translate-offset, 0));
			width: 180%;
			height: 180%;
			transition: transform 1000ms ease, opacity 1000ms ease;
			overflow: hidden;

			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
			}
			&.current--image {
				opacity: 1;
				--image-translate-offset: 0;
			}
			&.previous--image,
			&.next--image {
				opacity: 0;
			}
			&.previous--image {
				--image-translate-offset: -25%;
			}
			&.next--image {
				--image-translate-offset: 25%;
			}
		}
	}
}

.cardList {
	position: absolute;
	width: calc(3 * #{$card-width});
	height: auto;

	&__btn {
		--btn-size: 35px;
		width: var(--btn-size);
		height: var(--btn-size);
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		z-index: 100;

		&.btn--left {
			left: -5%;
		}
		&.btn--right {
			right: -5%;
		}

		.icon {
			width: 100%;
			height: 100%;
			svg {
				width: 100%;
				height: 100%;
			}
		}
	}

	.cards__wrapper {
		position: relative;
		width: 100%;
		height: 100%;
		perspective: 1000px;
	}
}

.card {
	--card-translateY-offset: 100vh;

	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%) translateX(var(--card-translateX-offset))
		translateY(var(--card-translateY-offset)) rotateY(var(--card-rotation-offset))
		scale(var(--card-scale-offset));
	display: inline-block;
	width: var(--card-width);
	height: var(--card-height);
	transition: transform var(--card-transition-duration)
		var(--card-transition-easing);
	user-select: none;
  box-shadow: 7px 5px 5px 1px #888888;

	&::before {
		content: "";
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background: #000;
		z-index: 1;
		transition: opacity var(--card-transition-duration)
			var(--card-transition-easing);
		opacity: calc(1 - var(--opacity));
	}

	&__image {
		position: relative;
		width: 100%;
		height: 100%;
		img {
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			object-fit: cover;
		}
	}

	&.current--card {
		--current-card-rotation-offset: 0;
		--card-translateX-offset: 0;
		--card-rotation-offset: var(--current-card-rotation-offset);
		--card-scale-offset: 1.2;
		--opacity: 0.8;
	}

	&.previous--card {
		--card-translateX-offset: calc(-1 * var(--card-width) * 1.1);
		--card-rotation-offset: 25deg;
	}

	&.next--card {
		--card-translateX-offset: calc(var(--card-width) * 1.1);
		--card-rotation-offset: -25deg;
	}

	&.previous--card,
	&.next--card {
		--card-scale-offset: 0.9;
		--opacity: 0.4;
	}
}


.infowalaList {
	position: absolute;
	width: calc(3 * #{$card-width});
  pointer-events: none;
	height: #{$card-height};

	.infowala__wrapper {
		position: relative;
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: flex-start;
		align-items: flex-end;
	perspective: 1000px;
	transform-style: preserve-3d;
	}
}
.infowalaLink {
  pointer-events: all;
}

.infowala {
	margin-bottom: calc(#{$card-height} / 8);
	margin-left: calc(#{$card-width} / 1.5);
	transform: translateZ(2rem);
	transition: transform #{$card-transition-duration}
		#{$card-transition-easing};
	.text {
		position: relative;
		font-family: "Montserrat";
		font-size: calc(#{$card-width} * var(--text-size-offset, 0.2));
		white-space: nowrap;
		color: #fff;
		width: fit-content;
	}

	.name,
	.location {
		text-transform: uppercase;
	}

	.location {
		font-weight: 800;
	}

	.location {
		--mg-left: 40px;
		--text-size-offset: 0.12;
		font-weight: 600;
		margin-left: var(--mg-left);
		margin-bottom: calc(var(--mg-left) / 2);
		padding-bottom: 0.8rem;
		&::before,
		&::after {
			content: "";
			position: absolute;
			background: #fff;
			left: 0%;
			transform: translate(calc(-1 * var(--mg-left)), -50%);
		}
		&::before {
			top: 50%;
			width: 20px;
			height: 5px;
		}
		&::after {
			bottom: 0;
			width: 60px;
			height: 2px;
		}
	}

	.description {
		--text-size-offset: 0.065;
		font-weight: 500;
	}

	&.current--infowala {
		opacity: 1;
		display: block;
	}
	&.previous--infowala,
	&.next--infowala {
		opacity: 0;
		display: none;
	}
}

.loading__wrapper {
	position: fixed;
	left: 0;
	top: 0;
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	background: #000;
	z-index: 200;
	.loader--text {
		color: #fff;
		font-family: "Montserrat";
		font-weight: 500;
		margin-bottom: 1.4rem;
	}
	.loader {
		position: relative;
		width: 200px;
		height: 2px;
		background: rgba(255, 255, 255, 0.25);
		span {
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			background: rgb(255, 0, 0);
			transform: scaleX(0);
			transform-origin: left;
		}
	}
}

@media only screen and (min-width: 800px) {
	:root {
		--card-width: 250px;
		--card-height: 400px;
	}
}

.support {
	position: absolute;
	right: 10px;
	bottom: 10px;
	padding: 10px;
	display: flex;
	a {
		margin: 0 10px;
		color: #fff;
		font-size: 1.8rem;
		backface-visibility: hidden;
		transition: all 150ms ease;
		&:hover {
			transform: scale(1.1);
		}
	}
}

</style>
