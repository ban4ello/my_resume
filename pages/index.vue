<template>
  <v-row justify="center" align="center" class="pa-4">
    <v-col>
      <div class="typeWiriter">
        <div class="d-flex start-flex">
          <h1>
            Hi everyone! I'm a
            <span class="typed-text" :class="{ lightMode }">{{ typeValue }}</span>
            <span class="blinking-cursor">|</span>
            <span class="cursor" :class="{ typing: typeStatus }">&nbsp;</span>
          </h1>
        </div>
        <div class="d-flex justify-center">
          <transition appear>
            <span
              v-show="showBtn"
              id="about"
              v-scroll-to="'#main-content'"
              color="accent"
              class="action-btn"
            >
              About me
            </span>
          </transition>
        </div>
      </div>

      <div id="main-content">
        <div class="summary_block large-margin">
          <v-row class="font-size-extra-large">
            <v-col>
              <h2>Summary</h2>
            </v-col>
          </v-row>

          <div class="d-flex justify-center gap-50">
            <div id="summary" class="d-flex flex-column justify-center">
              <h3 class="text-title bold mb-4">
                Ivan Miroshnichenko
              </h3>

              <p class="font-size-large">
                Hi! &#128075;&nbsp; My name is Ivan, I'm {{ new Date().getFullYear() - 1994 }} and I'm a front-end developer
                with a taste for knowledge, work and study, with a strong sense of aesthetics and teamwork
              </p>
            </div>

            <div>
              <img
                class="circle"
                :src="require('~/static/preview.jpg')"
              >
            </div>
          </div>
        </div>

        <div id="skills">
          <v-row class="font-size-extra-large">
            <v-col>
              <h2>Technical skills</h2>
            </v-col>
          </v-row>

          <div class="skills_block">
            <div class="d-flex flex-column justify-center">
              <p class="text-title bold mb-4">
                While working with web applications, I have worked with these technologies:
              </p>
            </div>

            <div class="items">
              <div class="items-col">
                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/html.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      HTML
                    </h3>
                    <span class="italic">its latest specifications.</span>
                  </div>
                </div>
                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/javascript.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      JavaScript
                    </h3>
                    <span class="italic">its latest specifications.</span>
                  </div>
                </div>
                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/react.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      React.js
                    </h3>
                    <span class="italic">used it, it scales well, I might use it again.</span>
                  </div>
                </div>
                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/blockchain.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      Blockchain
                    </h3>
                    <span class="italic">WEB3.0 is our future</span>
                  </div>
                </div>
              </div>

              <div class="items-col">
                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/css3.png')">
                  <h3 class="bold text-subtitle">
                    CSS, SASS, SCSS, LESS
                  </h3>
                </div>

                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/vue.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      VUE.JS, VUEX, NUXT.JS
                    </h3>
                    <span class="italic">because it is the best framework ever</span>
                  </div>
                </div>

                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/webpack.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      Webpack
                    </h3>
                    <span class="italic">but need to move on the Vite.js</span>
                  </div>
                </div>

                <div class="item">
                  <img width="120px" :src="require('~/assets/icons/git.png')">
                  <div>
                    <h3 class="bold text-subtitle">
                      GIT
                    </h3>
                    <span class="italic">where would we be without it in web development?</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <v-card id="hobby" color="secondary">
          <v-card-title class="headline ma-4">
            Hobby
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora beatae eum dignissimos, vel accusantium laboriosam natus corporis amet dolores adipisci? Dolor a iste dolorem excepturi, officia ea consectetur? Molestias, laborum?
          </v-card-text>
        </v-card>

        <v-card id="experience" color="secondary">
          <v-card-title class="headline ma-4">
            Working experience
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora beatae eum dignissimos, vel accusantium laboriosam natus corporis amet dolores adipisci? Dolor a iste dolorem excepturi, officia ea consectetur? Molestias, laborum?
          </v-card-text>
        </v-card>

        <v-card id="contacts" color="secondary">
          <v-card-title class="headline ma-4">
            Contacts
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora beatae eum dignissimos, vel accusantium laboriosam natus corporis amet dolores adipisci? Dolor a iste dolorem excepturi, officia ea consectetur? Molestias, laborum?
          </v-card-text>
        </v-card>
      </div>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',

  data () {
    return {
      typeValue: '',
      typeStatus: false,
      displayTextArray: ['person who loves programming...', 'creator...', 'Vue frontend developer.'],
      typingSpeed: 90,
      erasingSpeed: 30,
      newTextDelay: 1500,
      displayTextArrayIndex: 0,
      charIndex: 0,
      showBtn: false,
      timeoutId: null
    }
  },

  head () {
    const title = 'Ivan Miroshnichenko. Frontend Web Developer'
    const description = `I am Ivan. I'm ${new Date().getFullYear() - 1994} years old. And I really love developing software and electronic devices.`

    return {
      title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: description
        },
        {
          hid: 'key',
          name: 'key',
          content: 'main'
        },
        {
          hid: 'og:site_name',
          property: 'og:site_name',
          content: 'Ivan Miroshnichenko'
        },
        {
          hid: 'og:type',
          property: 'og:type',
          content: 'website'
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: title
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: description
        }
      ]
    }
  },

  computed: {
    lightMode () {
      return !this.$vuetify.theme.isDark
    }
  },

  created () {
    this.timeoutId = setTimeout(this.typeText, this.newTextDelay + 200)
  },

  methods: {
    typeText () {
      if (this.charIndex < this.displayTextArray[this.displayTextArrayIndex].length) {
        if (!this.typeStatus) { this.typeStatus = true }

        this.typeValue += this.displayTextArray[this.displayTextArrayIndex].charAt(
          this.charIndex
        )
        this.charIndex += 1
        setTimeout(this.typeText, this.typingSpeed)
      } else {
        this.typeStatus = false
        setTimeout(this.eraseText, this.newTextDelay)
      }
    },
    eraseText () {
      if (this.displayTextArrayIndex === 1) {
        // needed for the fastest appearance of the "about me" text
        this.newTextDelay = 100
      }
      if (this.displayTextArrayIndex + 1 >= this.displayTextArray.length && this.charIndex === this.displayTextArray[this.displayTextArrayIndex].length) {
        clearTimeout(this.timeoutId)

        this.showBtn = true

        return
      }

      if (this.charIndex > 0) {
        if (!this.typeStatus) { this.typeStatus = true }
        this.typeValue = this.displayTextArray[this.displayTextArrayIndex].substring(
          0,
          this.charIndex - 1
        )
        this.charIndex -= 1
        setTimeout(this.eraseText, this.erasingSpeed)
      } else {
        this.typeStatus = false
        this.displayTextArrayIndex += 1
        if (this.displayTextArrayIndex >= this.displayTextArray.length) { this.displayTextArrayIndex = 0 }

        setTimeout(this.typeText, this.typingSpeed + 500)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
  .typeWiriter {
    width: 100%;
    height: calc(100vh);
    display: flex;
    align-items: center;
    flex-direction: column;
    margin-top: 100px;

    .start-flex {
      align-items: flex-start;
      width: 100%;
      margin-bottom: 75px;
    }

    h1 {
      font-size: 5rem;
      font-weight: normal;
      span.typed-text {
        color: #d2b94b;

        &.lightMode {
          color: #064663;
        }
      }
    }
  }

  .skills_block {
    display: grid;
    grid-template-columns: 1fr;

    .items {
      display: flex;
      gap: 25px;
      justify-content: center;

      .items-col {
        display: flex;
        flex-direction: column;
        align-content: flex-start;
        gap: 25px;
      }

      .item {
        max-width: 450px;
        display: grid;
        gap: 15px;
        grid-template-columns: max-content 1fr;
        align-items: center;
      }
    }
  }

  .action-btn {
    font-size: 4em;
    text-decoration: underline;
    cursor: pointer;
  }

  .circle {
    border-radius: 50%;
    width: 400px;
    height: 400px;
    object-fit: cover;
  }

  @media screen and (max-width: 833px) {
    .typeWiriter {
      height: calc(100vh);
      align-items: center;
      margin-top: 20px;

      h1 {
        font-size: 4rem;
      }
    }

    .action-btn {
      font-size: 3em;
    }

    .large-margin {
      margin-bottom: 50px
    }
  }

  .gap-50 {
    gap: 50px;
  }
  .font-size-large {
    font-size: 1.5em;
  }
  .font-size-extra-large {
    font-size: 3em;
  }
  .text-title {
    font-size: 2em;
  }
  .text-subtitle {
    font-size: 1.5em;
  }
  .bold {
    font-weight: bold;
  }
  .italic {
    font-size: 1.5em;
    font-style: italic;
  }

  .large-margin {
    margin-bottom: 100px
  }

  // Cursor blinking CSS Starts...
  .blinking-cursor {
    font-size: 5rem;
    color: #2c3e50;
    -webkit-animation: 1s blink step-end infinite;
    -moz-animation: 1s blink step-end infinite;
    -ms-animation: 1s blink step-end infinite;
    -o-animation: 1s blink step-end infinite;
    animation: 1s blink step-end infinite;
  }
  @keyframes blink {
    from,
    to {
      color: transparent;
    }
    50% {
      color: #2c3e50;
    }
  }
  @-moz-keyframes blink {
    from,
    to {
      color: transparent;
    }
    50% {
      color: #2c3e50;
    }
  }
  @-webkit-keyframes blink {
    from,
    to {
      color: transparent;
    }
    50% {
      color: #2c3e50;
    }
  }
  @-ms-keyframes blink {
    from,
    to {
      color: transparent;
    }
    50% {
      color: #2c3e50;
    }
  }
  @-o-keyframes blink {
    from,
    to {
      color: transparent;
    }
    50% {
      color: #2c3e50;
    }
  }
  // Cursor blinking CSS Ends...

// transition animation for "about me" text
.v-enter-active {
  transition: all 1s ease-out;
}

.v-enter {
  transform: translateX(20px);
  opacity: 0;
}
</style>
