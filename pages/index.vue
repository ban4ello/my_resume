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

      <div id="main-content" class="main" :class="screen">
        <div class="summary_block large-margin">
          <TitleBlock name="Summary 👨‍💻" />

          <div class="d-flex justify-center gap-50">
            <div id="summary" class="d-flex flex-column justify-center">
              <h3 class="text-title bold mb-4">
                Ivan Miroshnichenko
              </h3>

              <p class="font-size-large">
                <span class="emoji wave icon-size" />&nbsp; I'm <span class="info--text bold">{{ myExactAge }}</span>&nbsp; years old and I'm a front-end developer
                with a taste for knowledge, work and study, with a strong sense of aesthetics and teamwork
              </p>
            </div>

            <div class="d-flex align-center">
              <img
                width="400px"
                height="400px"
                class="circle mobile-view"
                :src="require('~/static/preview.jpg')"
              >
            </div>
          </div>
        </div>

        <div id="skills" class="large-margin">
          <TitleBlock name="🤹 Technical skills" class="mb-8" />

          <div class="skills_block">
            <div class="d-flex justify-center flex-column align-center mb-8">
              <p class="text-title bold mb-12">
                While working with web applications, I have worked with these technologies:
              </p>

              <ShadowRoundBtn
                v-if="!showActivateBtn && (screen !== 'sm' && screen !== 'xs')"
                btn-text="Click for fun"
                @click="activateBomb()"
              />
              <ShadowRoundBtn
                v-if="showActivateBtn && showResetBtn && (screen !== 'sm' && screen !== 'xs')"
                btn-text="Reset"
                @click="reset()"
              />
            </div>

            <div ref="skills_block_parent" class="grid-col">
              <div v-if="showBomb && !showExplode" class="bomb">
                <img width="200px" :src="require('~/assets/images/bomb.gif')">
              </div>
              <div v-if="showExplode" style="position: absolute; top: -3%; left: 20%;">
                <img width="600px" :src="require('~/assets/images/explode.gif')">
              </div>

              <TextImageBlock
                v-for="(item, i) in technicalSkillsArray"
                ref="skills_block_items"
                :key="i"
                :title="item.title"
                :subtitle="item.subtitle"
                :image-name="item.imageName"
                class=""
              />
            </div>
          </div>
        </div>

        <div id="experience" class="large-margin">
          <TitleBlock name="Working experience 🛠️" class="mb-8" />

          <v-timeline>
            <v-timeline-item
              v-for="(item, i) in experienceList"
              :key="i"
              :color="item.color"
              small
            >
              <template #opposite>
                <span
                  :class="`headline font-weight-bold ${item.color}--text`"
                  v-text="item.year"
                />
              </template>
              <div class="py-4">
                <span :class="`text-title mb-4 ${item.color}--text`">
                  {{ item.experience.title }}
                </span>

                <p class="font-size-large">
                  {{ item.experience.text }}
                </p>

                <div v-if="item.experience.responsibilities.length" class="font-size-large">
                  <p class="info--text">
                    Responsibilities:
                  </p>
                  <ul class="responsibilities-list">
                    <li v-for="(item, i) in item.experience.responsibilities" :key="i">
                      {{ item }}
                    </li>
                  </ul>
                </div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </div>

        <div id="hobby" class="large-margin">
          <TitleBlock name="🎯 Hobby" class="mb-8" />

          <div class="hobby_block">
            <div class="items large-margin">
              <div class="items-col">
                <h3 class="bold text-title">
                  I independently develop automation devices, Smart home systems and some extraordinary devices.
                </h3>
                <h3 class="bold text-title">
                  When developing, I use microcontrollers famalys: Atmel AVR (tinyAVR, megaAVR): RISC-V (ESP32/8266) and IoT
                </h3>
                <h3 class="bold text-title">
                  I program microcontrollers on C++ (with AVR-libs), js (used the Johnny-Five framework, executed in Node.js), used the "Mongoose OS" framework for ESP MC).
                </h3>
              </div>

              <div class="items-row">
                <img width="100px" :src="require('~/assets/icons/smart-home.png')">
                <img width="100px" :src="require('~/assets/icons/diy.png')">
                <img width="100px" :src="require('~/assets/icons/microcontroller.png')">
                <img width="100px" :src="require('~/assets/icons/microprocessor.png')">
                <img width="100px" :src="require('~/assets/icons/nodejs.png')">
                <img width="100px" :src="require('~/assets/icons/c.png')">
              </div>
            </div>

            <div class="d-flex justify-center flex-column align-center">
              <h3 class="text-title info--text">
                I also like to play chess <span class="icon-size">♛</span>. You can challenge me.
              </h3>
              <h3 class="text-title">
                Link for invitation : <a class="info--text" href="https://chess.com/play/ban4ello" target="_blank">fight me in chess</a>
              </h3>
            </div>
          </div>
        </div>

        <div id="contacts" class="large-margin">
          <TitleBlock name="Contacts 📞" class="mb-8" />

          <div class="contacts_block">
            <a class="item link" href="mailto:ban4ellog@gmail.com" target="_blank">
              <img width="100px" :src="require('~/assets/icons/email.png')">
              <h3 class="bold text-title">
                E-mail
              </h3>
            </a>
            <a class="item link" href="https://github.com/ban4ello" target="_blank">
              <img width="100px" :src="require('~/assets/icons/github.png')">
              <h3 class="bold text-title">
                Github
              </h3>
            </a>
            <a class="item link" href="https://www.linkedin.com/in/ivan-miroshnichenko-36b003190/" target="_blank">
              <img width="100px" :src="require('~/assets/icons/linkedin.png')">
              <h3 class="bold text-title">
                Linkedin
              </h3>
            </a>
          </div>
        </div>

        <div class="email-form">
          <div class="d-flex gap-4" style="display: flex; flex-direction: column; align-items: center; margin-bottom: 20px;">
            <h2>Заказать звонок</h2>
            <h4>Оставьте заявку и наш менеджер перезвонит Вам!</h4>
          </div>

          <input v-model="emailName" type="text" name="name" placeholder="Ваше имя:">
          <input v-model="emailPhone" type="text" name="phone" placeholder="Ваш телефон:">

          <button :disabled="!emailAccess" @click="sendEmail()" class="email-form-btn">
            Заказать звонок
          </button>

          <div style="
            display: flex;
            max-height: 30px;
            align-items: center;
            align-content: center;
            gap: 10px;
          ">
            <input v-model="emailAccess" type="checkbox" id="horns" name="horns" style="width: max-content;" />
            <label for="horns">Я согласен(а) с условиями передачи информации</label>
          </div>
        </div>
      </div>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',

  data () {
    return {
      emailName: '',
      emailPhone: '',
      emailAccess: true,
      showBomb: false,
      showExplode: false,
      showActivateBtn: false,
      showResetBtn: false,
      myExactAge: '30 years',
      technicalSkillsArray: [
        {
          imageName: 'javascript',
          title: 'JavaScript',
          subtitle: 'its latest specifications'
        },
        {
          imageName: 'html',
          title: 'HTML',
          subtitle: 'its latest specifications'
        },
        {
          imageName: 'css3',
          title: 'CSS, Vuetify, Bootstrap, Tailwind',
          subtitle: 'SASS, LESS preprocessor'
        },
        {
          imageName: 'vue',
          title: 'VUE.JS, VUEX, NUXT.JS',
          subtitle: 'because it is the best framework ever'
        },
        {
          imageName: 'api',
          title: 'REST API, gRPC, Swagger',
          subtitle: ''
        },
        {
          imageName: 'jest',
          title: 'Unit, e2e testing',
          subtitle: 'Jest, Cypress'
        },
        {
          imageName: 'webpack',
          title: 'Webpack, Vite.js',
          subtitle: ''
        },
        {
          imageName: 'agile',
          title: 'Agile methodology (SCRUM)',
          subtitle: 'Jira, Trello, Figma'
        },
        {
          imageName: 'git',
          title: 'GIT',
          subtitle: 'where would we be without it in web development?'
        }
      ],
      experienceList: [
        {
          color: 'disabled',
          year: 'mid 2018 - 2019',
          experience: {
            title: 'Self-study of web technologies',
            text: '',
            responsibilities: []
          }
        },
        {
          color: 'info',
          year: '2019 - 2020',
          experience: {
            title: 'WOK-email',
            text: 'App for creating responsive HTML-email',
            responsibilities: [
              'development of app interface using Vue.js and Element.io by Figma layouts',
              'work on creating an internal library based on MJML',
              'e2e testing with Cypress.io, unit testing with Jest'
            ]
          }
        },
        {
          color: 'info',
          year: '2020 - sep 2020',
          experience: {
            title: '[noname] startup',
            text: 'Application for learning foreign languages',
            responsibilities: [
              'development of an admin panel using Vue.js and Vuetify UI',
              'bug fixing, project support'
            ]
          }
        },
        {
          color: 'info',
          year: 'sep 2020 - oct 2022',
          experience: {
            title: 'EventScouts',
            text: 'Decentralized app for searching events and activities using WEB 3.0',
            responsibilities: [
              'development of app interface using Vue.js and Vuetify UI by Figma layouts',
              'development of a decentralized app (according to the mobile first strategy)',
              'optimization, implementation of new functions on Vue.js (development using the Scrum methodology)',
              'evaluation and execution of threaded tasks',
              'interaction with backend (REST API)'
            ]
          }
        },
        {
          color: 'info',
          year: 'nov 2022 - sep 2023',
          experience: {
            title: 'Altessa Solutions',
            text: 'Web, mobile & desktop app development, UI/UX design experts - professional solutions of your business',
            responsibilities: [
              'development of app interface using Vue.js by Figma layouts',
              'optimization, implementation of new functions on Vue.js (Nuxt.js)',
              'development using the Scrum methodology',
              'evaluation and execution of threaded tasks',
              'interaction with backend (gRPC API)'
            ]
          }
        },
        {
          color: 'info',
          year: 'oct 2022 - current time',
          experience: {
            title: 'Manzana Group',
            text: 'Management system for loyalty programs in retail, insurance, banking, healthcare and sports',
            responsibilities: [
              'development of app interface using Vue.js',
              'optimization, implementation of new functions',
              'development of internal UI library components',
              'code review',
              'interaction with a large team of developers: backend (REST API), business analytics, QA engineers'
            ]
          }
        }
      ],
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
      script: [
        {
          src: 'https://smtpjs.com/v3/smtp.js'
        },
        {
          type:'text/javascript',
        }
      ],
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
    calculatedAge () {
      return new Date().getFullYear() - new Date('07.01.1994').getFullYear()
    },

    screen () {
      return this.$vuetify.breakpoint.name
    },

    lightMode () {
      return !this.$vuetify.theme.isDark
    }
  },

  created () {
    this.timeoutId = setTimeout(this.typeText, this.newTextDelay + 200)
    setInterval(this.ageCalculator, 1000)
  },

  methods: {
    sendEmail () {
      const dateOfReport = new Date().toDateString() + ' ' + new Date().getHours() + ':' + new Date().getMinutes()
      const body = `
        <h1>Дата и время заявки: </h1>${dateOfReport}
        <h1>Имя: </h1>${this.emailName}
        <br>
        <h1>Телефон: </h1>${this.emailPhone}
      `;

      Email.send({
        SecureToken: "3dcaf62d-5eed-484a-89f1-6e4693bdbc71",
        To: 'ban4ellog@gmail.com',
        From: "ban4ellog@gmail.com",
        Subject: 'Заявка на обратный звонок: ' + dateOfReport,
        Body: body
      }).then((message, error) => {
        if (message === 'OK') {
          console.log("Заявка отправлена успешно!");
          alert("Заявка отправлена успешно!")
        } else {
          console.log(message, error);
          alert("Упс! Что-то пошло не так. Попробуйте позже")
        }

        this.emailName = null;
        this.emailPhone = null;
      });
    },

    getRandomInt (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)

      return Math.floor(Math.random() * (max - min) + min)
    },

    activateBomb (event) {
      this.showActivateBtn = true
      this.showBomb = true
      const coordinates = []
      const parentCoord = this.$refs.skills_block_parent.getBoundingClientRect()

      this.$refs.skills_block_parent.style.width = parentCoord.width + 'px'
      this.$refs.skills_block_parent.style.height = parentCoord.height + 'px'

      this.$refs.skills_block_items.forEach((item, i) => {
        coordinates.push({ top: item.$el.offsetTop + 'px', left: item.$el.offsetLeft + 'px' })
      })

      const sectors = {
        a: {
          x: { start: 0, end: Math.round(parentCoord.width / 2) },
          y: { start: 0, end: Math.round(parentCoord.height / 2) }
        },
        b: {
          x: { start: Math.round(parentCoord.width / 2), end: parentCoord.width },
          y: { start: 0, end: Math.round(parentCoord.height / 2) }
        },
        c: {
          x: { start: 0, end: Math.round(parentCoord.width / 2) },
          y: { start: Math.round(parentCoord.height / 2), end: parentCoord.height }
        },
        d: {
          x: { start: Math.round(parentCoord.width / 2), end: parentCoord.width },
          y: { start: Math.round(parentCoord.height / 2), end: parentCoord.height }
        }
      }

      this.$refs.skills_block_items.forEach((item, i) => {
        item.$el.style.position = 'absolute'
        item.$el.style.transition = '0.4s'
        item.$el.style.top = coordinates[i].top
        item.$el.style.left = coordinates[i].left
      })

      setTimeout(() => {
        this.showExplode = true
      }, 2400)

      setTimeout(() => {
        this.$refs.skills_block_items.forEach((item, i) => {
          const clientX = parseInt(item.$el.style.left)
          const clientY = parseInt(item.$el.style.top)

          Object.keys(sectors).forEach((sectorName) => {
            if (
              (clientX >= sectors[sectorName].x.start && clientX <= sectors[sectorName].x.end) &&
              (clientY >= sectors[sectorName].y.start && clientY <= sectors[sectorName].y.end)
            ) {
              item.sector = sectorName
            }
          })

          if (item.sector === 'a') {
            item.$el.style.left = (clientX - sectors[item.sector].x.start - clientY - this.getRandomInt(50, 150)) + 'px'
            item.$el.style.top = (clientY - sectors[item.sector].y.start - this.getRandomInt(50, 150)) + 'px'
          }

          if (item.sector === 'b') {
            item.$el.style.left = clientX + this.getRandomInt(100, 500) + 'px'
            item.$el.style.top = sectors[item.sector].y.start - this.getRandomInt(0, 150) + 'px'
          }

          if (item.sector === 'c') {
            item.$el.style.left = clientX - this.getRandomInt(0, 300) + 'px'
            item.$el.style.top = clientY + this.getRandomInt(100, 400) + 'px'
          }

          if (item.sector === 'd') {
            item.$el.style.left = clientX + this.getRandomInt(100, 400) + 'px'
            item.$el.style.top = clientY + this.getRandomInt(10, 300) + 'px'
          }

          item.$el.style.transform = `rotate(${this.getRandomInt(-50, 50)}deg)`
        })

        this.showBomb = false
        this.showResetBtn = true
      }, 2500)

      setTimeout(() => {
        this.showExplode = false
      }, 3000)
    },

    reset () {
      this.$refs.skills_block_items.forEach((item, i) => {
        item.$el.style.top = '0px'
        item.$el.style.left = '0px'
        item.$el.style.transform = 'rotate(0deg)'
        item.$el.style.position = 'inherit'
      })

      this.showResetBtn = false
    },

    ageCalculator () {
      const now = new Date()
      const exactBirthDate = '01/07/1994/07:10' // mm-dd-yyyy-mm-ss
      const months = exactBirthDate.slice(0, 2)
      const days = Number(exactBirthDate.slice(3, 5))
      const years = exactBirthDate.slice(6, 10)
      const exactTime = Number(exactBirthDate.slice(11, 13))
      const exactMinutes = Number(exactBirthDate.slice(14, 16))

      const birthDate = new Date(`${months}/${days + 1}/${years}`)
      const hours = now.getHours() - exactTime
      const minutes = now.getMinutes() - exactMinutes
      const seconds = now.getSeconds()
      const endingDate = new Date().toISOString().substr(0, 10) // YYYY-MM-DD

      let startDate = new Date(birthDate.toISOString().substr(0, 10))
      let endDate = new Date(endingDate)

      if (startDate > endDate) {
        const swap = startDate
        startDate = endDate
        endDate = swap
      }

      const startYear = startDate.getFullYear()
      const february = (startYear % 4 === 0 && startYear % 100 !== 0) || startYear % 400 === 0 ? 29 : 28
      const daysInMonth = [31, february, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

      let yearDiff = endDate.getFullYear() - startYear
      let monthDiff = endDate.getMonth() - startDate.getMonth()
      let dayDiff = endDate.getDate() - startDate.getDate()

      if (monthDiff < 0) {
        yearDiff--
        monthDiff += 12
      }

      if (dayDiff < 0) {
        if (monthDiff > 0) {
          monthDiff--
        } else {
          yearDiff--
          monthDiff = 11
        }
        dayDiff += daysInMonth[startDate.getMonth()]
      }

      this.myExactAge = `${yearDiff} years, ${monthDiff} months, ${dayDiff} days, ${hours < 0 ? 0 : hours} hours : ${minutes < 0 ? 0 : minutes} minutes : ${seconds} seconds`
    },

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
.grid-col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 25px;
  margin: 0 auto;
  margin-bottom: 20px;
  position: relative;
}
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

.action-btn {
  font-size: 4em;
  text-decoration: underline;
  cursor: pointer;
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

@media screen and (max-width: 600px) {
  .typeWiriter h1 {
    font-size: 2.5rem;
  }

  .action-btn {
    font-size: 2em;
  }

  .grid-col {
    grid-template-columns: 1fr;
  }
}

.main {
  &.md {
    .mobile-view {
      width: 300px;
      height: 300px;
    }

    .font-size-extra-large {
      font-size: 2em;
    }

    .text-title {
      font-size: 1.5em;
    }
  }

  &.sm {
    .mobile-view {
      width: 250px;
      height: 250px;
    }
  }

  &.xs {
    .skills_block,
    .hobby_block {
      .items {
        flex-direction: column;
      }
    }
    .contacts_block {
      display: flex;
      justify-content: center;
      flex-direction: row;
      gap: 20px;
      flex-wrap: wrap;
    }
    .font-size-extra-large {
      font-size: 1.5em;
    }
    .text-title {
      font-size: 1em;
    }
    .mobile-view {
      width: 150px;
      height: 150px;
    }
    .font-size-large {
      font-size: 0.8em;
    }
    .italic {
      font-size: 1em;
    }
  }

  .skills_block,
  .hobby_block {
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
      .items-row {
        display: flex;
        flex-direction: row;
        grid-gap: 25px;
        gap: 25px;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
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

  .contacts_block {
    display: flex;
    justify-content: space-between;

    .item {
      display: flex;
      align-items: center;
      gap: 15px;
    }
  }

  .circle {
    border-radius: 50%;
    object-fit: cover;
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
    margin-bottom: 100px;
  }
  .icon-size {
    font-size: 1.7em;
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

.emoji::after {
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}

.wave::after {
  content: '✋';
  --emoji: '👋';
  animation-name: twoFrames;
  animation-duration: 0.8s;
}

@keyframes twoFrames {
  50% {
    content: var(--emoji);
  }
}
.bomb {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  position: absolute;
  top: 30%;
  left: 40%;
}

.responsibilities-list {
  font-style: italic;

  li {
    list-style-type: '👉';
    padding-left: 2ch;
  }
}

</style>

<style lang="scss">
.v-application .link {
  color: #fff !important;
  text-decoration: none;
}

.email-form {
  width: 500px;
  background-color: #fff;
  color: #000;
  padding: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 25px;
  margin: 0 auto;
  margin-bottom: 40px;
  
  input {
    padding: 5px 15px;
    margin-top: 5px;
    border: 1px solid #ccc;
    resize: none;
    color: #000;
    width: 100%;
    border-radius: 15px;
  }
  
  button {
    margin-top: 10px;
    padding: 5px 10px;
    background-color: #FFEB3B;
    border: none;
    color: #000;
    cursor: pointer;
    width: 100%;
    border-radius: 15px;
    margin-bottom: 35px;
    font-weight: 800;
  }

  button:disabled,
  button[disabled]{
    opacity: 0.5;
    cursor: not-allowed;
  }
}
</style>
