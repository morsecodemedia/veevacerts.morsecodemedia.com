<template>
  <div class="vae-tech-v2">
    <h1>Approved Email Technical Certification</h1>
    <div class="filter-menu">
      <label>
        Live Search
        <input
          v-model="filter"
          type="text"
          class="code-filter"
          placeholder="Type here to search questions and answers."
        >
      </label>
      <div v-if="filter" class="filter-results">
        <div class="result-num">
          There
          <span v-if="resultNum > 1">are</span>
          <span v-if="resultNum == 1">is</span>
          <mark>{{ resultNum }}</mark>
          <span v-if="resultNum > 1">results</span>
          <span v-if="resultNum == 1">result</span>
          that
          <span v-if="resultNum > 1">match</span>
          <span v-if="resultNum == 1">matches</span>
          your keyword.
        </div>
        <button class="clear-btn" @click="filter = ''">
          CLEAR FILTER
        </button>
      </div>
    </div>
    <div
      v-if="filteredQ.length"
      id="vae"
    >
      <p>Showing {{ filteredQ.length }} of {{ questions.length }}</p>
      <table border="1" cellspacing="0" cellpadding="10">
        <tbody>
          <tr v-for="q in filteredQ" :key="q.question">
            <td colspan="2">
              <span class="question" v-html="q.question" />
              <table cellspacing="0" cellpadding="10">
                <tr v-for="a in q.answers" :key="a.option" class="answer-row">
                  <td>
                    <label>
                      <input
                        type="checkbox"
                        :checked="a.valid === 'Correct'"
                        disabled
                      >
                      {{ a.option }}
                    </label>
                  </td>
                </tr>
              </table>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { vae } from '~/static/vae.json'
export default {
  name: 'VAETechV2',
  data () {
    return {
      filter: '',
      questions: vae
    }
  },
  head () {
    return {
      title: 'Approved Email Technical v2 - Veeva Certs | A morsecodemedia tool',
      meta: [
        {
          hid: 'ogtitle',
          property: 'og:title',
          content: 'Approved Email Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'twtitle',
          name: 'twitter:title',
          content: 'Approved Email Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'googlename',
          itemprop: 'name',
          content: 'Approved Email Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'description',
          name: 'description',
          content: 'A tool for studying for Veeva certifications.'
        },
        {
          hid: 'ogdescription',
          property: 'og:description',
          content: 'A tool for studying for Veeva certifications.'
        },
        {
          hid: 'twdescription',
          name: 'twitter:description',
          content: 'A tool for studying for Veeva certifications.'
        },
        {
          hid: 'googledescription',
          itemprop: 'description',
          content: 'A tool for studying for Veeva certifications.'
        },
        {
          hid: 'ogurl',
          property: 'og:url',
          content: 'https://veevacerts.morsecodemedia.com' + this.$route.path
        },
        {
          hid: 'twsite',
          name: 'twitter:site',
          content: 'https://veevacerts.morsecodemedia.com' + this.$route.path
        }
      ],
      link: [
        {
          hid: 'canonical',
          rel: 'canonical',
          href: 'https://veevacerts.morsecodemedia.com' + this.$route.path
        }
      ]
    }
  },
  computed: {
    filteredQ () {
      return this.questions
        .filter(b =>
          b.question.toLowerCase().includes(this.filter.toLowerCase())
        )
        .map((b) => {
          const a = { question: b.question, answers: b.answers }
          if (this.filter) {
            const re = new RegExp(this.filter, 'i')
            a.question = a.question.replace(
              re,
              '<mark>' + this.filter + '</mark>'
            )
          }
          return a
        })
    },
    resultNum () {
      return this.filteredQ.length
    }
  }
}
</script>

<style lang="scss">
.vae-tech-v2 {
  max-width: 900px;
  margin: 30px auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  p {
    margin-bottom: 30px;
  }
}
.question {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 15px;
}
.answer-row {
  padding: 0 10px;
  label {
    font-size: 18px;
    padding: 5px 0;
    width: 100vw;
    max-width: 900px;
    display: flex;
  }
  td {
    border-bottom: 1px solid #ccc;
  }
}
input[type="text"] {
  padding: 5px 15px;
  font-size: 18px;
  display: block;
  width: 100vw;
  max-width: 900px;
  margin-bottom: 5px;
}
input[type="checkbox"] {
  margin-right: 10px;
  height: 20px;
  width: 20px;
}
</style>
