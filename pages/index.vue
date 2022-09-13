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
        <v-card id="summary" color="secondary">
          <v-card-title class="headline ma-4">
            Summary
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora beatae eum dignissimos, vel accusantium laboriosam natus corporis amet dolores adipisci? Dolor a iste dolorem excepturi, officia ea consectetur? Molestias, laborum?
          </v-card-text>
        </v-card>

        <v-card id="skills" color="secondary">
          <v-card-title class="headline ma-4">
            Technical skills
          </v-card-title>

          <v-card-text>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora beatae eum dignissimos, vel accusantium laboriosam natus corporis amet dolores adipisci? Dolor a iste dolorem excepturi, officia ea consectetur? Molestias, laborum?
          </v-card-text>
        </v-card>

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
      if (this.displayTextArrayIndex + 1 >= this.displayTextArray.length && this.charIndex === this.displayTextArray[this.displayTextArrayIndex].length) {
        clearTimeout(this.timeoutId)

        setTimeout(() => {
          this.showBtn = true
        }, 0)

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

  .action-btn {
    font-size: 4em;
    text-decoration: underline;
  }

  @media screen and (max-width: 833px) {
    .typeWiriter {
      height: calc(100vh);
      align-items: center;

      h1 {
        font-size: 4rem;
      }
    }

    .action-btn {
      font-size: 3em;
    }
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
