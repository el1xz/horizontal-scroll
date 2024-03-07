<template>
  <LocomotiveScroll ref="scroller" class="scroll-container" :getted-options="{ smooth: true }" @init="locomotive = $refs.scroller.locomotive">
    <div>
    <section data-bgcolor="#bcb8ad" data-textcolor="#032f35">
      <div>
        <h1 data-scroll data-scroll-speed="1"><span>Horizontal</span> <span>scroll</span> <span>section</span></h1>
        <p data-scroll data-scroll-speed="2" data-scroll-delay="0.2">with GSAP ScrollTrigger & Locomotive Scroll</p>
      </div>
    </section>

    <section id="sectionPin">
      <div class="pin-wrap">
        <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</h2>
        <img src="https://images.unsplash.com/photo-1682685797886-79020b7462a4?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="">
        <img src="https://images.unsplash.com/photo-1709223328664-f3c5f94a8e70?q=80&w=2038&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="">
        <img src="https://images.unsplash.com/photo-1709487577432-9238a48c5a58?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="">

      </div>
    </section>
    <section data-bgcolor="#e3857a" data-textcolor="#f1dba7"><img src="https://images.unsplash.com/photo-1709603945846-6901ed447ecd?q=80&w=2129&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="">
      <h2 data-scroll data-scroll-speed="1" class="credit"><a href="https://codepen.io/cameronknight/pen/qBNvrRQ" target="_blank">Horizontal Effect by Advantage</a></h2>
      <h2 data-scroll data-scroll-speed="1" class="credit"><a href="https://github.com/DidoMarchet/starter-kit-nuxt-locomotive-scroll" target="_blank">Locomotive setup by DidoMarchet</a></h2>
      <h2 data-scroll data-scroll-speed="1" class="credit"><a href="https://github.com/el1xz" target="_blank">Edit by el1xz</a></h2>
    </section>
  </div>
  </LocomotiveScroll>
</template>

<script>
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

export default {
  name: 'IndexPage',
  data: () => ({
    locomotive: undefined,
  }),
  head() {
    return {
      title: 'Horizontal Scroll',
    }
  },
  watch: {
    locomotive: {
      handler() {
        this.locomotive.on('scroll', ScrollTrigger.update)
        const locomotive = this.locomotive
        ScrollTrigger.scrollerProxy(locomotive.el, {
          scrollTop(value) {
            return arguments.length
              ? locomotive.scrollTo(value, 0, 0)
              : locomotive.scroll.instance.scroll.y
          },
          getBoundingClientRect() {
            return {
              top: 0,
              left: 0,
              width: window.innerWidth,
              height: window.innerHeight,
            }
          },
          pinType: document.querySelector('.scroll-container').style.transform
            ? 'transform'
            : 'fixed',
        })

        const elements = document.querySelectorAll('#sectionPin')
        elements.forEach((element) => this.elementAnimation(element))
      },
    },
  },
  methods: {
    elementAnimation(element) {
      const pinWrap = document.querySelector(".pin-wrap");
      const pinWrapWidth = pinWrap.offsetWidth;
      const horizontalScrollLength = pinWrapWidth - window.innerWidth;
      gsap.to('.pin-wrap', {
        scrollTrigger: {
          trigger: element,
          scroller: this.$refs.scroller.locomotive.el,
          scrub: true,
          pin: true,
          start: 'top top',
          end: pinWrapWidth,
        },
        x: -horizontalScrollLength,
        ease: 'none',
      });
      ScrollTrigger.addEventListener("refresh", () => this.locomotive.update());
      ScrollTrigger.refresh();
    },
  },
}
</script>

<style>
:root {
  --text-color: #111;
  --bg-color: #b9b3a9;
}

body {
  font-family: termina, sans-serif;
  color: var(--text-color);
  background: var(--bg-color);
  transition: 0.3s ease-out;
  overflow-x: hidden;
  max-width: 100%;
  width: 100%;
  overscroll-behavior: none;
}

section:not(#sectionPin) {
  min-height: 100vh;
  width: 100%;
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 2rem;
  padding: 50px 10vw;
  margin: auto;
  place-items: center;
}

img {
  height: 80vh;
  width: auto;
  object-fit: cover;
}

h1 {
  font-size: 5rem;
  line-height: 1;
  font-weight: 800;
  margin-bottom: 1rem;
  position: absolute;
  top: 10vw;
  left: 10vw;
  z-index: 4;
  overflow-wrap: break-word;
  hyphens: auto;

  @media (max-width: 768px) {
    font-size: 16vw;
  }

  span {
    display: block;
  }
}

h2 {
  font-size: 2rem;
  max-width: 400px;
}

.credit {
  font-family: Termina, sans-serif;
  a {
    color: var(--text-color);
  }
}

* {
  box-sizing: border-box;
}

#sectionPin {
  height: 100vh;
  overflow: hidden;
  display: flex;
  left: 0;
  background: var(--text-color);
  color: var(--bg-color);
}

.pin-wrap {
  height: 100vh;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 50px 10vw;

  & > * {
    min-width: 60vw;
    padding: 0 5vw;
  }
}

p {
  position: absolute;
  bottom: 10vw;
  right: 10vw;
  width: 200px;
  line-height: 1.5;
}

</style>
