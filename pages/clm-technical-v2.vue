<template>
  <div class="clm-tech-v2">
    <h1>Veeva CLM Technical Certification</h1>
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
      v-if="filteredCLM.length"
      id="clm"
    >
      <p>Showing {{ filteredCLM.length }} of {{ clm.length }}</p>
      <table border="1" cellspacing="0" cellpadding="10">
        <tbody>
          <tr v-for="q in filteredCLM" :key="q.question">
            <td colspan="2">
              <span class="question" v-html="q.question" />
              <table cellspacing="0" cellpadding="10">
                <tr v-for="a in q.answers" :key="a.option" class="answer-row">
                  <label>
                    <input
                      type="checkbox"
                      :checked="a.valid === 'Correct'"
                      disabled
                    >
                    {{ a.option }}
                  </label>
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
export default {
  name: 'CLMTechV2',
  data () {
    return {
      filter: '',
      clm: [
        {
          question: 'The Custom Reaction Buttons use how many pixels?',
          answers: [
            {
              option: '160x37',
              valid: 'Correct'
            },
            {
              option: '154x36',
              valid: 'Incorrect'
            },
            {
              option: '170x40',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'When the Navigation Bar displays during a CLM Presentation, it is possible to conceal the content above the Navigation Bar through the configuration.',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following can be disabled within CLM?',
          answers: [
            {
              option: 'The swipe motion for slide navigation',
              valid: 'Correct'
            },
            {
              option: 'The Action Button',
              valid: 'Incorrect'
            },
            {
              option:
                'The exit button if all slides have not been viewed in a presentation',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'What items are tracked "Out of the box"?',
          answers: [
            {
              option: 'Presentation name',
              valid: 'Correct'
            },
            {
              option: 'Display order',
              valid: 'Correct'
            },
            {
              option: 'Version',
              valid: 'Correct'
            },
            {
              option: 'Start time',
              valid: 'Correct'
            },
            {
              option: 'Duration on a slide',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'On which device types does Veeva support Augmented Reality?',
          answers: [
            {
              option: 'iPhone',
              valid: 'Incorrect'
            },
            {
              option: 'iPad',
              valid: 'Correct'
            },
            {
              option: 'Windows',
              valid: 'Incorrect'
            },
            {
              option: 'Android',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Wide Content tracks which of the following?',
          answers: [
            {
              option: 'Only the first Key Message of a CLM Presentation',
              valid: 'Incorrect'
            },
            {
              option: 'Each Key Message on the Call Report',
              valid: 'Correct'
            },
            {
              option: 'All clikcs on the Call Report',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which statement describes Deep Content?',
          answers: [
            {
              option:
                'All slides or pages in a presentations are hosted in an individual file loaded as a single Key Message',
              valid: 'Correct'
            },
            {
              option:
                'Each slide or page in a presentation is an individual file loaded as a separate Key Message',
              valid: 'Incorrect'
            },
            {
              option:
                'Many slides or pages in many presentations shared by many Key Messages',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Do Content Creators need to prepare media to be loaded into Vault PromotMats?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Ideal content design should be which of the following?',
          answers: [
            {
              option:
                'Use a mixture of deep and wide philosophies depending on needs',
              valid: 'Correct'
            },
            {
              option: 'Wide Content Design Philosophy',
              valid: 'Incorrect'
            },
            {
              option: 'Deep Content Design Philosophy',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which statement describes Wide Content?',
          answers: [
            {
              option:
                'Many slides or pages in many presentations shared by many Key Messages',
              valid: 'Incorrect'
            },
            {
              option:
                'All slides or pages in a presentation are hosted in an individual file loaded as a single Key Message',
              valid: 'Incorrect'
            },
            {
              option:
                'Each slide or page in a presentation is an individual file loaded as a separate Key Message',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Can CLM Content be flagged as training material?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the following Veeva JavaScript methods allow you access to a Hidden Presentation?',
          answers: [
            {
              option: 'getDataforObject',
              valid: 'Incorrect'
            },
            {
              option: 'gotoSlide',
              valid: 'Correct'
            },
            {
              option: 'launchSlide',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Can a Key Message be viewed in Portrait?',
          answers: [
            {
              option:
                'Yes, but only if the Rotation Lock has been disabled for the given Key Message',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Select all the Native Resolution Options?',
          answers: [
            {
              option: 'Scale to 2048x1536',
              valid: 'Incorrect'
            },
            {
              option: 'Scale to Fit',
              valid: 'Correct'
            },
            {
              option: 'Scale to 1024x768',
              valid: 'Correct'
            },
            {
              option: 'Default for Device',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Select the native CLM functions that can be disabled?',
          answers: [
            {
              option: 'History Button',
              valid: 'Correct'
            },
            {
              option: 'Action Menu',
              valid: 'Incorrect'
            },
            {
              option: 'Navigation Bar',
              valid: 'Correct'
            },
            {
              option: 'Swipe',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'For Legacy Packaging, is it possible to include stylesheet files?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Can you upload ZIP files larger than 500MB?',
          answers: [
            {
              option: 'Yes, if they are compressed',
              valid: 'Incorrect'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes, but onlyu with FTP',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Is it possible to create Key Messages directly in Veeva CRM?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Is it possible to migrate CLM Content from one Veeva CRM instance to another Veeva CRM instance?',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Is it possible to create a CLM Presentation directly in Veeeva CRM?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following statements are true',
          answers: [
            {
              option:
                'HTML Content can contain HTML, images, fonts, CSS and JavaScript',
              valid: 'Correct'
            },
            {
              option:
                'HTML Content can only contain an index.html and thumb.png',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Can CLM content be previewed in Valut',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'For HTML Content which files must be included in the ZIP file?',
          answers: [
            {
              option: 'thumb.jpg',
              valid: 'Incorrect'
            },
            {
              option: 'thumb.png',
              valid: 'Correct'
            },
            {
              option: 'index.html',
              valid: 'Correct'
            },
            {
              option: 'default.html',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'HTML CLM content must be compressed into a ZIP file',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Excluding HTML, what other typed of content can be packaged and loaded?',
          answers: [
            {
              option: 'PDF',
              valid: 'Correct'
            },
            {
              option: 'PowerPoint',
              valid: 'Correct'
            },
            {
              option: 'Image',
              valid: 'Correct'
            },
            {
              option: 'Video',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'What is the maximum number of documents that can be changed at once by a bulk document action',
          answers: [
            {
              option: '500',
              valid: 'Incorrect'
            },
            {
              option: '2000',
              valid: 'Incorrect'
            },
            {
              option: '10',
              valid: 'Incorrect'
            },
            {
              option: '1000',
              valid: 'Correct'
            },
            {
              option: '1',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Can you use Bulk Actions to add Multichannel Slides to a Multichannel Presentation?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Is it possible to have multiple versions of a document in Vault PromoMats?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Select the 2 ways to add a new version of a document to Vault PromoMats',
          answers: [
            {
              option: 'Upload a new version of a document',
              valid: 'Correct'
            },
            {
              option: 'Update document',
              valid: 'Incorrect'
            },
            {
              option: 'Create a document draft',
              valid: 'Correct'
            },
            {
              option: 'Supersede document',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which 2 ways can you download assets from Vault PromoMats?',
          answers: [
            {
              option: 'Vault Export',
              valid: 'Incorrect'
            },
            {
              option: 'Binder Export',
              valid: 'Correct'
            },
            {
              option: 'Multichannel Exporter',
              valid: 'Incorrect'
            },
            {
              option: 'Bulk Document Export',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Can you use the Multichannel Loader to load Required Slides?',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Can you use the Multichannel Loader for Auto Packaging?',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Incorrect'
            },
            {
              option: 'Yes, when the correct fields are populated',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Please select the documents that are used by the Multichannel Loader?',
          answers: [
            {
              option: 'Access Database',
              valid: 'Incorrect'
            },
            {
              option: 'CSV File',
              valid: 'Correct'
            },
            {
              option: 'Document ZIP files',
              valid: 'Correct'
            },
            {
              option: 'Viewable Rendition Files',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which export options are available in Vault PromoMats',
          answers: [
            {
              option: 'CLM Export',
              valid: 'Incorrect'
            },
            {
              option: 'Binder Export',
              valid: 'Correct'
            },
            {
              option: 'Bulk Document Export',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following are examples of use cases for the Vault PromoMats Multichannel Loader?',
          answers: [
            {
              option: 'Synchronise content on the iPad',
              valid: 'Incorrect'
            },
            {
              option: 'Update ZIP source files for slides',
              valid: 'Correct'
            },
            {
              option: 'Update document fileds',
              valid: 'Correct'
            },
            {
              option: 'Creating presentations and slides',
              valid: 'Correct'
            },
            {
              option: 'Add slides to presentations',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Is it possible to integrate a survey into a CLM Presentation?',
          answers: [
            {
              option: 'No',
              valid: 'Incorrect'
            },
            {
              option: 'Yes',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'In order to make a survey available to a Rep what is the final step?',
          answers: [
            {
              option: 'Created',
              valid: 'Incorrect'
            },
            {
              option: 'Launched',
              valid: 'Incorrect'
            },
            {
              option: 'Published',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Survey Branching is available via which channels?',
          answers: [
            {
              option: 'Vault PromoMats',
              valid: 'Incorrect'
            },
            {
              option: 'CRM',
              valid: 'Correct'
            },
            {
              option: 'CLM',
              valid: 'Correct'
            },
            {
              option: 'Approved Email',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Survey Branching is available on which of the following platforms?',
          answers: [
            {
              option: 'Android',
              valid: 'Incorrect'
            },
            {
              option: 'iPhone',
              valid: 'Correct'
            },
            {
              option: 'CRM Online',
              valid: 'Correct'
            },
            {
              option: 'Windows',
              valid: 'Incorrect'
            },
            {
              option: 'iPad',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'On which platforms can you complete a survey?',
          answers: [
            {
              option: 'Windows Tablet',
              valid: 'Correct'
            },
            {
              option: 'iPhone',
              valid: 'Correct'
            },
            {
              option: 'Android',
              valid: 'Incorrect'
            },
            {
              option: 'iPad',
              valid: 'Correct'
            },
            {
              option: 'CRM Online',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following Veeva JavaScript methods are used to get Survey Data in HTML?',
          answers: [
            {
              option: 'getSurveyTarget_Account',
              valid: 'Incorrect'
            },
            {
              option: 'getquestionResponse_SurveyTarget',
              valid: 'Correct'
            },
            {
              option: 'getSurveyQuestions_Survey',
              valid: 'Incorrect'
            },
            {
              option: 'getDataforCurrentObject("Survey")',
              valid: 'Correct'
            },
            {
              option: 'accessSurveyQuestions',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Survey Branching allows for conditional questuions based on previous answer choices.',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'For Survey Branching, Parent questions can be which of the following types?',
          answers: [
            {
              option: 'Text',
              valid: 'Incorrect'
            },
            {
              option: 'Number',
              valid: 'Incorrect'
            },
            {
              option: 'Picklist',
              valid: 'Correct'
            },
            {
              option: 'Radio',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following Veeva JavaScript methods are used to add or update Survey Data in HTML?',
          answers: [
            {
              option: 'createSurvey',
              valid: 'Incorrect'
            },
            {
              option: 'updateSurvey',
              valid: 'Incorrect'
            },
            {
              option: 'createRecord',
              valid: 'Correct'
            },
            {
              option: 'updateRecord',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Does Survey Overlay need to be configured?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which two fields must be populated to enable the Survey Overlay page to display in CLM?',
          answers: [
            {
              option: 'The Enable Survey Overlay field must equal yes',
              valid: 'Correct'
            },
            {
              option:
                'Populate the Survey lookup field with the correct Survey',
              valid: 'Correct'
            },
            {
              option: 'The Enbale Survey overlay field must equal no',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Can the Survey Overlay be used without selecting an Account?',
          answers: [
            {
              option: 'No',
              valid: 'Correct'
            },
            {
              option: 'Yes',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'When Survey Branching is used, will the HCP see the child questions when the Survey initially loads on the page?',
          answers: [
            {
              option: 'Yes',
              valid: 'Incorrect'
            },
            {
              option: 'No',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Veeva CRM on Windows is supported on which of the following?',
          answers: [
            {
              option: 'Windows 8',
              valid: 'Incorrect'
            },
            {
              option: 'Windows 10 Professional',
              valid: 'Correct'
            },
            {
              option: 'Windows 10 Enterprise',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Do legacy CLM API functions work on Windows?',
          answers: [
            {
              option: 'Yes',
              valid: 'Incorrect'
            },
            {
              option: 'No',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'What is the supported resolution on Windows?',
          answers: [
            {
              option: '1920x1080',
              valid: 'Correct'
            },
            {
              option: '1024x768',
              valid: 'Incorrect'
            },
            {
              option: '2048x1536',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Are there considerations when naming files for Windows?',
          answers: [
            {
              option: 'Yes',
              valid: 'Correct'
            },
            {
              option: 'No',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'What is the aspect ratio of Windows?',
          answers: [
            {
              option: '16:9',
              valid: 'Correct'
            },
            {
              option: '4:3',
              valid: 'Incorrect'
            },
            {
              option: '12:9',
              valid: 'Incorrect'
            }
          ]
        }
      ]
    }
  },
  head () {
    return {
      title: 'CLM Technical v2 - Veeva Certs | A morsecodemedia tool',
      meta: [
        {
          hid: 'ogtitle',
          property: 'og:title',
          content: 'CLM Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'twtitle',
          name: 'twitter:title',
          content: 'CLM Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'googlename',
          itemprop: 'name',
          content: 'CLM Technical v2 - Veeva Certs | A morsecodemedia tool'
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
    filteredCLM () {
      return this.clm
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
      return this.filteredCLM.length
    }
  }
}
</script>

<style lang="scss">
.clm-tech-v2 {
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
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 15px;
}
.answer-row {
  padding: 0 10px;
  label {
    font-size: 18px;
    margin-bottom: 10px;
    padding: 5px 0;
    width: 100vw;
    max-width: 900px;
    display: flex;
    border-bottom: 1px solid #ccc;
  }
}
input[type="text"] {
  padding: 5px 15px;
  font-size: 18px;
}
input[type="checkbox"] {
  margin-right: 10px;
}
.filter-menu {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
