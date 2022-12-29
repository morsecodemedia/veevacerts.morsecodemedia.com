<template>
  <div class="engage-tech-v2">
    <h1>Engage Meeting Technical Certification</h1>
    <div class="filter-menu">
      <label>
        Live Search
        <input
          v-model="filter"
          type="text"
          class="code-filter"
          placeholder="Type here to search questions and answers."
        />
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
        <button class="clear-btn" @click="filter = ''">CLEAR FILTER</button>
      </div>
    </div>
    <div v-if="filteredQ.length" id="engage">
      <p>Showing {{ filteredQ.length }} of {{ engage.length }}</p>
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
                      />
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
export default {
  name: 'EngageTechV2',
  data () {
    return {
      filter: '',
      engage: [
        {
          question:
            'Up to how many attendees can be added while hosting an Engage Meeting?',
          answers: [
            {
              option: '5',
              valid: 'Incorrect'
            },
            {
              option: '15',
              valid: 'Incorrect'
            },
            {
              option: '25',
              valid: 'Correct'
            },
            {
              option: '35',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Engage Meeting requires a specific Veeva license to run.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Engage Meeting supports video calling.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'From which tab can we monitor users who have Engage Meeting licenses?',
          answers: [
            {
              option: 'CLM Administration Tab',
              valid: 'Incorrect'
            },
            {
              option: 'Engage Metadata Administration Tab',
              valid: 'Incorrect'
            },
            {
              option: 'Engage Content Administration Tab',
              valid: 'Incorrect'
            },
            {
              option: 'Engage Meeting Administration Tab',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'What is the correct Email Template Type that needs to be set in Vault for configuring an Approved Email invitation for an Engage Meeting?',
          answers: [
            {
              option: 'Standard Template',
              valid: 'Incorrect'
            },
            {
              option: 'CoBrowse Invite Template',
              valid: 'Incorrect'
            },
            {
              option: 'Remote Meeting Invite Template',
              valid: 'Correct'
            },
            {
              option: 'Events Management Invite Template',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'For uploading a Splash Screen in CRM which record type needs to be selected under the HTML Reports Tab?',
          answers: [
            {
              option: 'Account',
              valid: 'Incorrect'
            },
            {
              option: 'Remote Meeting',
              valid: 'Correct'
            },
            {
              option: 'KOL Profile',
              valid: 'Incorrect'
            },
            {
              option: 'Splash Screen',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which Token needs to be used for generating an .ics file corresponding to an Engage Meeting tghat can be later downloaded by HCPs?',
          answers: [
            {
              option: '{{Call2_vod__c.Call_Datetime_vod__c}}',
              valid: 'Incorrect'
            },
            {
              option:
                '{{Call2_vod__c.Parent_Call_vod__r.Call_Datetime_vod__c}}',
              valid: 'Incorrect'
            },
            {
              option: '{{addToCalendar}}',
              valid: 'Correct'
            },
            {
              option: '{{iCalendar}}',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Engage Meeting Media Player only supports CLM content sourced from Vault.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the following all web clients support two-way video between a Rep and an HCP participating in an Engage Meeting joined via a web browser?',
          answers: [
            {
              option: 'Chrome',
              valid: 'Correct'
            },
            {
              option: 'Firefox',
              valid: 'Correct'
            },
            {
              option: 'Safari',
              valid: 'Correct'
            },
            {
              option: 'Edge',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Engage Meetings can be conducted via iPad and Windows Desktop.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which Javascript method is NOT supported in Engage Meeting content created for Desktops?',
          answers: [
            {
              option: 'gotoSlide',
              valid: 'Incorrect'
            },
            {
              option: 'createRecord',
              valid: 'Incorrect'
            },
            {
              option: 'queryRecord',
              valid: 'Correct'
            },
            {
              option: 'getDataForCurrentObject',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the below CLM functionalities are supported for CRM Engage Media Player? (Select all that apply)',
          answers: [
            {
              option: 'Required Slides',
              valid: 'Correct'
            },
            {
              option: 'Shared Resources',
              valid: 'Correct'
            },
            {
              option: 'Hidden Presentations',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following CLM functionalities are supported for CRM Engage Media Player?',
          answers: [
            {
              option: 'Required Slides',
              valid: 'Correct'
            },
            {
              option: 'Shared Resources',
              valid: 'Correct'
            },
            {
              option: 'Hidden Presentations',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'In the CRM Engage App Media Library, which of the following are valid statuses for the presentations?',
          answers: [
            {
              option: 'Approved',
              valid: 'Incorrect'
            },
            {
              option: 'Download Required',
              valid: 'Correct'
            },
            {
              option: 'Update Pending',
              valid: 'Correct'
            },
            {
              option: 'Downloaded',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Call Key Message records get automatically created for a key message if viewed longer than how many seconds in the CRM Engage Player?',
          answers: [
            {
              option: '1 second',
              valid: 'Incorrect'
            },
            {
              option: '2 seconds',
              valid: 'Correct'
            },
            {
              option: '3 seconds',
              valid: 'Incorrect'
            },
            {
              option: '4 seconds',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'What type of files are supported and can be used during an Engage Meeting presentation?',
          answers: [
            {
              option: 'HTML',
              valid: 'Correct'
            },
            {
              option: 'PDF',
              valid: 'Correct'
            },
            {
              option: 'Video',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Should we directly make use of available CLM content for an Engage Meeting without testing?',
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
            'Which Javascript method supported in Engage Meeting content created for an iPad?',
          answers: [
            {
              option: 'getDataForCurrentObject',
              valid: 'Inorrect'
            },
            {
              option: 'gotoSlide',
              valid: 'Incorrect'
            },
            {
              option: 'nextSlide',
              valid: 'Incorrect'
            },
            {
              option: 'createMultichannelActivityLine',
              valid: 'Incorrect'
            },
            {
              option: 'All of the above',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which Javascript method is supported in Engage Meeting content created for an iPad?',
          answers: [
            {
              option: 'getDataForCurrentObject',
              valid: 'Correct'
            },
            {
              option: 'gotoSlide',
              valid: 'Correct'
            },
            {
              option: 'nextSlide',
              valid: 'Correct'
            },
            {
              option: 'createMultichannelActivityLine',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following field on Call object distinguishes a Detail call from a Remote Meeting call?',
          answers: [
            {
              option: 'Remote_Meeting__c',
              valid: 'Incorrect'
            },
            {
              option: 'Remote_Meeting_vod__c',
              valid: 'Correct'
            },
            {
              option: 'Veeva_Remote_Meeting_Id__c',
              valid: 'Incorrect'
            },
            {
              option: 'Veeva_Remote_Meeting_id_vod__c',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Content uploaded via this technique should work perfectly in Engage Meeting? (Select all that apply)',
          answers: [
            {
              option: 'FTP upload in CRM',
              valid: 'Incorrect'
            },
            {
              option: 'Create Presentation in Vault',
              valid: 'Correct'
            },
            {
              option: 'Legacy packaging methodology',
              valid: 'Incorrect'
            },
            {
              option: 'Single Doc Publishing',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Content created via Vault\'s Create Presentation and Single-Doc Publishing will render correctly in the CRM Engage media player.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'What Vault document type should be selected when creating an Engage Meeting slide in Vault?',
          answers: [
            {
              option: 'Product Information',
              valid: 'Incorrect'
            },
            {
              option: 'Multichannel Presentation',
              valid: 'Incorrect'
            },
            {
              option: 'Multichannel Slide',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'During an Engage Meeting which of the following applies?',
          answers: [
            {
              option: 'Presenter speaks only',
              valid: 'Incorrect'
            },
            {
              option:
                'Attendees are able to speak and interact with the presenter',
              valid: 'Correct'
            },
            {
              option: 'Presenter and co-presenter speaks only',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Splash Screen displays for the HCPs when the host is not viewing CLM content and is viewing other parts of CRM.',
          answers: [
            {
              option: 'False',
              valid: 'Incorrect'
            },
            {
              option: 'True',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Which of the following JavaScript functions are supported by Engage Meeting hosted from the Desktop?',
          answers: [
            {
              option: 'nextSlide() / prevSlide()',
              valid: 'Correct'
            },
            {
              option: 'updateCurrentRecord() / createRecord()',
              valid: 'Correct'
            },
            {
              option: 'createMultichannelActivityLine()',
              valid: 'Incorrect'
            },
            {
              option: 'gotoSlide() / gotoSlideV2()',
              valid: 'Correct'
            },
            {
              option: 'getDataForCurrentObject()',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Your agency is creating a HTML slide, after creating the files according to the Vault Packaging structure which statement is true?',
          answers: [
            {
              option: 'Set the files inside a folder and then zip the folder',
              valid: 'Incorrect'
            },
            {
              option: 'All files and folders must be zipped from the root',
              valid: 'Correct'
            },
            {
              option:
                'Zipping the files is not necessary as Vault will auto-populate them',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'When used in an Engage Meeting invite, what does the .ics file do?',
          answers: [
            {
              option: 'Creates a claendar reminder',
              valid: 'Correct'
            },
            {
              option: 'Allows attendee to review the meeting recording',
              valid: 'Incorrect'
            },
            {
              option: 'Downloads the Engage Meeting app',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Engage Meeting Licenses are assigned by groups.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Engage Meeting Content follows the regular CLM upload process when uploading to Vault.',
          answers: [
            {
              option: 'False',
              valid: 'Incorrect'
            },
            {
              option: 'True',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Is it best practice to directly make use of available CLM content for an Engage Meeting with no testing.',
          answers: [
            {
              option: 'True',
              valid: 'Incorrect'
            },
            {
              option: 'False',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'What type of files are supported and can be used during an Engage Meeting presentation?',
          answers: [
            {
              option: 'HTML and PDF',
              valid: 'Correct'
            },
            {
              option: 'PDF and Videos',
              valid: 'Incorrect'
            },
            {
              option: 'Videos only',
              valid: 'Incorrect'
            },
            {
              option: 'HTML and Videos',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'If an administrator tries to access the Engage Administration tab and gets an error, what may be happening?',
          answers: [
            {
              option: 'The browser doesn\'t support it',
              valid: 'Incorrect'
            },
            {
              option:
                'There are too many people trying to access at the same time',
              valid: 'Incorrect'
            },
            {
              option: 'Licenses have not been provisioned',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'What Vault document type should be selected when creating an Engage Meeting presentation in Vault?',
          answers: [
            {
              option: 'Promotional Material',
              valid: 'Incorrect'
            },
            {
              option: 'Multichannel Presentation',
              valid: 'Correct'
            },
            {
              option: 'Approved Document',
              valid: 'Incorrect'
            },
            {
              option: 'Multichannel Slide',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which object can the Splash Screen read information from?',
          answers: [
            {
              option: 'Account_voc',
              valid: 'Incorrect'
            },
            {
              option: 'User_vod',
              valid: 'Incorrect'
            },
            {
              option: 'User_Detail_vod',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'The Splash Screen is defined by the administrator in the CLM Media Library.',
          answers: [
            {
              option: 'False',
              valid: 'Correct'
            },
            {
              option: 'True',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'How many licenses are provisioned to an agency upon request?',
          answers: [
            {
              option: '2',
              valid: 'Correct'
            },
            {
              option: '5',
              valid: 'Incorrect'
            },
            {
              option: 'As many as they want',
              valid: 'Incorrect'
            },
            {
              option: '3',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Media content viewed in the CRM Engage app during an Engage Meeting is tracked on the Call.',
          answers: [
            {
              option: 'False',
              valid: 'Incorrect'
            },
            {
              option: 'True',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'For an HTML slide, following the Vault Packaging structure, what should be the namer of the HTML file?',
          answers: [
            {
              option: 'slide.html',
              valid: 'Incorrect'
            },
            {
              option: 'source.html',
              valid: 'Incorrect'
            },
            {
              option: 'vault.html',
              valid: 'Incorrect'
            },
            {
              option: 'index.html',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Engage Meeting can be scheduled from the Call Report.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'We do not recommend using Legacy Packaging for Engage Meeting CLM content.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Is it possible to track CLM contnet displayed from an Engage Meeting?',
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
          question: 'How can an agency request Engage Meeting licenses?',
          answers: [
            {
              option: 'Licenses are assigned by default',
              valid: 'Incorrect'
            },
            {
              option: 'By sending a request to their Program Manager',
              valid: 'Correct'
            },
            {
              option: 'By logging a ticket via the Support Website',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Is it possible to host group calls in Engage Meeting?',
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
            'It is possible to enable or disable features on a channel basis when creating CLM content.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Who is responsible for assigning Engage Meeting licenses to Users?',
          answers: [
            {
              option: 'The System Administrator',
              valid: 'Correct'
            },
            {
              option: 'The End User',
              valid: 'Incorrect'
            },
            {
              option: 'The Veeva Team',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the following packages would be acceptable according to the Vault Package structure?',
          answers: [
            {
              option:
                'engage_slide.zip > index.html, thumb.png, js (folder), CSS (folder)',
              valid: 'Correct'
            },
            {
              option:
                'engage_slide.zip > index.html, images.png, js (folder), CSS (folder)',
              valid: 'Incorrect'
            },
            {
              option:
                'engage_slide > engage_slide.html, engage_slide-thumb.png',
              valid: 'Incorrect'
            },
            {
              option:
                'engage_slide (folder) > engage_slide.zip > index.html, image.png, js (folder), CSS (folder)',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the following packages would be acceptable according to the Vault Package structure?',
          answers: [
            {
              option:
                'my_slide.zip > thumb.png, index.html, js (folder), CSS (folder), img (folder)',
              valid: 'Correct'
            },
            {
              option:
                'my_slide.zip > thumb.png, my_slide.html, js (folder), CSS (folder)',
              valid: 'Incorrect'
            },
            {
              option: 'my_slide.zip > thumb.png, index.html, myfunctions.js',
              valid: 'Correct'
            },
            {
              option:
                'engage_slide.zip > myslide (folder) > index.html, image.png, js (folder), CSS (folder)',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Regarding the JavaScript library, select all that apply:',
          answers: [
            {
              option:
                'All CLM JavaScript functions are supported by Engage Meeting hosted from the iPad',
              valid: 'Correct'
            },
            {
              option:
                'Some JavaScript functions are supported by Engage Meeting hosted from the iPad',
              valid: 'Incorrect'
            },
            {
              option:
                'JavaScript is not supported by Engage Meeting when hosted from Desktop',
              valid: 'Incorrect'
            },
            {
              option:
                'Some JavaScript functions are supported by Engage Meeting hosted from the Desktop',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Exisxting CLM HTML content generally needs to be adapted to render correctly on the CRM Engage desktop Media Library.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'What Token should be used in order to add the Meeting Date and Time to the Invitation?',
          answers: [
            {
              option: '{{Call_DateTime_vod__c}}',
              valid: 'Incorrect'
            },
            {
              option: '{{Date_and_time}}',
              valid: 'Incorrect'
            },
            {
              option: '{{Call2_vod__c.Call_Datetime_vod__C}}',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'The Splash Screen can be customised',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'In The CRM Engage App Media Library, which of the following are valid statements regarding the presentations?',
          answers: [
            {
              option: 'Waiting Approval',
              valid: 'Incorrect'
            },
            {
              option: 'Downloaded',
              valid: 'Correct'
            },
            {
              option: 'Download Required',
              valid: 'Correct'
            },
            {
              option: 'Update Pending',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'You are creating an Engage Meeting Approved Email invitation, which tokens would you use to add Date, Time, URL, and calendar reminder in a comprehensive format?',
          answers: [
            {
              option:
                '{{parentCallDateTime}} / {{Call2_vod__c.Cobrowse_URL_Participant_vod__c}} / {{addToCalendar}}',
              valid: 'Correct'
            },
            {
              option:
                '{{Call2_vod__c.Call_Datetime_vod__c}} / {{URL}} / {{addIcsFile}}',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'What Token should be used in order to add the Meeting URL to the Invitation?',
          answers: [
            {
              option: '{{URL}}',
              valid: 'Incorrect'
            },
            {
              option: '{{Call2_vod__c.Cobrowse_URL_Participant_vod__c}}',
              valid: 'Correct'
            },
            {
              option: '{{Call2_vod__c.URL}}',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'HCPs can join an Engage Meeting from whivch of the following?',
          answers: [
            {
              option: 'Browser only',
              valid: 'Incorrect'
            },
            {
              option: 'iPhone only',
              valid: 'Incorrect'
            },
            {
              option: 'Any device',
              valid: 'Correct'
            },
            {
              option: 'iPad only',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'How can you add an Engage Meeting calendar reminder to an Approved Email?',
          answers: [
            {
              option:
                'By adding the meeting to the agenda, it creates automatically',
              valid: 'Incorrect'
            },
            {
              option:
                'By flagging the option "send reminder" from the call report',
              valid: 'Incorrect'
            },
            {
              option:
                'By adding the token {{addToCalendar}} to the invitation template',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Content uploaded via <nobr>__________</nobr> will work perfectly in Engage Meeting.',
          answers: [
            {
              option: 'Legacy packaging methodology',
              valid: 'Incorrect'
            },
            {
              option: 'FTP upload in CRM',
              valid: 'Incorrect'
            },
            {
              option: 'Create Presentation in Vault',
              valid: 'Correct'
            },
            {
              option: 'Single Doc Publishing',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'We recommend that you upload Engage Meeting Content directly into CRM',
          answers: [
            {
              option: 'False',
              valid: 'Correct'
            },
            {
              option: 'True',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Which of the following are considered best practices for building content for Engage Meeting when hosted from a Desktop?',
          answers: [
            {
              option: 'Use relative sizes for images',
              valid: 'Correct'
            },
            {
              option: 'Consider SVG for images and icons',
              valid: 'Correct'
            },
            {
              option: 'Not to use CSS',
              valid: 'Incorrect'
            },
            {
              option: 'Use and size content to the viewport',
              valid: 'Correct'
            }
          ]
        },
        {
          question:
            'Engage Meeting Media Player only supports CLM content sourced from Vault',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'In order to run a meeting from your desktop (Windows 7 or newer), the host should have the Veeva CRM Engage Meeting application downloaded on the machine',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Video content of any type does not display to participants when:',
          answers: [
            {
              option: 'Hosting from Windows desktop only',
              valid: 'Incorrect'
            },
            {
              option: 'Hosting from both an iPad or Windows Desktop',
              valid: 'Correct'
            },
            {
              option: 'Hosting from an iPad only',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Engage Meeting Hosted from the Desktop is launched from the Call Report.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Content displayed in an Engage Meeting can be tracked.',
          answers: [
            {
              option: 'True',
              valid: 'Correct'
            },
            {
              option: 'False',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'A Presentation shared in Engage Meeting can be which of the following?',
          answers: [
            {
              option: 'Regular CLM Presentations',
              valid: 'Correct'
            },
            {
              option: 'A Binder from Vault',
              valid: 'Correct'
            },
            {
              option: 'A pdf file hosted in the user\'s desktop or iPad',
              valid: 'Incorrect'
            },
            {
              option: 'A set of images hosted in the custoemr server',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'Engage Meeting can be hosted from which of the following devices?',
          answers: [
            {
              option: 'Android Device',
              valid: 'Incorrect'
            },
            {
              option: 'Windows Desktop',
              valid: 'Correct'
            },
            {
              option: 'iPad',
              valid: 'Correct'
            },
            {
              option: 'Windows Tablet',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question:
            'What action is required in order for Engage Metting calls to be stored in Veeva CRM?',
          answers: [
            {
              option: 'A special API must be installed',
              valid: 'Incorrect'
            },
            {
              option: 'Special integration must be built from scratch',
              valid: 'Incorrect'
            },
            {
              option: 'Nothing, it is automaticallyu captured in Veeva CRM',
              valid: 'Correct'
            }
          ]
        }
      ]
    }
  },
  head () {
    return {
      title:
        'Engage Meeting Technical v2 - Veeva Certs | A morsecodemedia tool',
      meta: [
        {
          hid: 'ogtitle',
          property: 'og:title',
          content:
            'Engage Meeting Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'twtitle',
          name: 'twitter:title',
          content:
            'Engage Meeting Technical v2 - Veeva Certs | A morsecodemedia tool'
        },
        {
          hid: 'googlename',
          itemprop: 'name',
          content:
            'Engage Meeting Technical v2 - Veeva Certs | A morsecodemedia tool'
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
      return this.engage
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

<style lang='scss'>
.engage-tech-v2 {
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
input[type='text'] {
  padding: 5px 15px;
  font-size: 18px;
  display: block;
  width: 100vw;
  max-width: 900px;
  margin-bottom: 5px;
}
input[type='checkbox'] {
  margin-right: 10px;
  height: 20px;
  width: 20px;
}
</style>
