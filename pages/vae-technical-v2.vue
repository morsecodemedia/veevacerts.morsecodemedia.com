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
      <p>Showing {{ filteredQ.length }} of {{ vae.length }}</p>
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
export default {
  name: 'VAETechV2',
  data () {
    return {
      filter: '',
      vae: [
        {
          question: 'Fill in with the right word: Reference Documents and Materials (Promotional Pieces) reside in Vault PromoMats and are not synced to Veeva CRM. When the email recipient clicks through to view the document, they will always see the <nobr>__________</nobr> version of that document which is approved in Vault PromoMats.',
          answers: [
            {
              option: 'latest',
              valid: 'Correct'
            },
            {
              option: 'oldest',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'The steps required to upload Approved Email content to Vault PromoMats are: <br> 1. Create a new Approved Email document by uploading the HTML file and completing the metadata <br> 2. Upload Reference Documents and Materials <br> 3. Create relationships: <br> - Email Template - Email Fragment(s), Template Fragment and <br> - Email Template, Email Fragment - Reference Document(s), Material (Promotional Piece(s) <br> 4. Approve Reference Documents and Materials (Promotional Pieces) <br> 5. Approve (or Stage) Email Templates, Email Fragments and Template Fragments <br> 6. Perform a sync in Veeva CRM to publish content and meta-data to Veeva CRM',
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
          question: 'When filling out metadata fields in Vault, the required fields are highlighted in:',
          answers: [
            {
              option: 'Orange',
              valid: 'Incorrect'
            },
            {
              option: 'Red',
              valid: 'Inorrect'
            },
            {
              option: 'Yellow',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Approved Emails are normally triggered automatically based on the behaviour of the HCP.',
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
          question: 'Configuration Tokens allow personalization of Approved Emails by merging data from Veeva CRM and/or allowing Users to customise the content of the email before it is sent.',
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
          question: 'In Vault, in the "From" and "Reply To" fields it is not possible to hardcode to a specific email address.',
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
          question: 'Industry standard best practices for developing HTML emails should be adhered to when creating Approved Email content. Which of the following should also be considered:',
          answers: [
            {
              option: 'Keep it simple',
              valid: 'Correct'
            },
            {
              option: 'Use Approved Email as a marketing tool',
              valid: 'Incorrect'
            },
            {
              option: 'Personalize',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'It is possible to define the exact Email Fragments that should be available to insert into each Email Template.',
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
          question: 'When creating a new Email Template, the metadata needs to include the email header information. Which of the following fields can be optional when populating under the "Email Properties" section of the document information in Vault PromoMats?',
          answers: [
            {
              option: 'From Name',
              valid: 'Correct'
            },
            {
              option: 'From Address',
              valid: 'Incorrect'
            },
            {
              option: 'Reply To Address',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following links generated from a token can be selected and viewed whilst in Preview or Edit Mode:',
          answers: [
            {
              option: '{{$VaultDocID}}',
              valid: 'Correct'
            },
            {
              option: '{{AppDocID}}',
              valid: 'Correct'
            },
            {
              option: '{{Account.Id}}',
              valid: 'Correct'
            },
            {
              option: '{{userName}}',
              valid: 'Incorrect'
            },
            {
              option: '{{ISILink}}',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Capturing HCP actions or requests from an Approved Email is done by creating a Multichannel Activity record using which of the following tokens?',
          answers: [
            {
              option: '{{parentCallDatetime}}',
              valid: 'Incorrect'
            },
            {
              option: '{{approvedEmailAction}}',
              valid: 'Correct'
            },
            {
              option: '{{approved_Email_Action}}',
              valid: 'Incorrect'
            },
            {
              option: '##approvedEmailAction##',
              valid: 'Incorrect'
            },
            {
              option: '{{requiresReview}}',
              valid: 'Incorrect'
            },
            {
              option: '{{EmailAction}}',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Approved Email can be used to send out links to Engage for Portals content. This is achieved by inserting <nobr>__________</nobr> Configuration Token into the HTML of the Email Template or Email Fragment.',
          answers: [
            {
              option: '{{addToCalendar}}',
              valid: 'Incorrect'
            },
            {
              option: '{{approvedEmailAction}}',
              valid: 'Incorrect'
            },
            {
              option: '{{engageLink}}',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Before syncing Vault PromoMats and Veeva CRM, Email Template, Email Fragment and Template Fragment documents must be set to either "Staged" or "Approved".',
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
          question: 'Approved Email can not be triggered to launch directly from a CLM Presentation.',
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
          question: 'When an End User sends an Approved Email, the values of the Subject Line, and free text or rich text entered by the sender are never recorded.',
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
          question: 'Approved Emails can be marked as requiring additional review before being sent to recipients by adding the <nobr>__________</nobr> token to the appropriate content.',
          answers: [
            {
              option: '{{requiresReview}}',
              valid: 'Correct'
            },
            {
              option: '{{approvedEamilAction}}',
              valid: 'Incorrect'
            },
            {
              option: '{{parentCallDatetime}}',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Approved Email users can select and view some links generated from a token while in Preview or Edit Mode. A new browser window opens displaying the web page when selecting a link.',
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
          question: 'Which of the following ensures the HCP Account can receive an Approved Email?',
          answers: [
            {
              option: 'Ensure that the "Approved Email Admin" checkbox is ticked on the User record',
              valid: 'Incorrect'
            },
            {
              option: 'Set the "Approved Email Test Email Address" to the User\'s own email address',
              valid: 'Incorrect'
            },
            {
              option: 'Set the "Approved Email Consent" field to "Implicit Opt In" or create an opt in (Multichannel Consent) record for that Account',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following can be inserted into an Email Template by an end user (e.g. a sales rep)?',
          answers: [
            {
              option: 'Template Fragment',
              valid: 'Incorrect'
            },
            {
              option: 'Email Fragment',
              valid: 'Correct'
            },
            {
              option: 'Master Email Fragment',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following can be inserted in an Email Template by using Custom Text Tokens?',
          answers: [
            {
              option: 'A picklist with fixed text options',
              valid: 'Correct'
            },
            {
              option: 'A picklist of images',
              valid: 'Incorrect'
            },
            {
              option: 'A free text field with default text',
              valid: 'Correct'
            },
            {
              option: 'A blank free text field',
              valid: 'Correct'
            },
            {
              option: 'A picklist with dynamic text options (using Merge Tokens)',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Custom Text Tokens can be used to provide end users with which of the following?',
          answers: [
            {
              option: 'A placeholder to insert images',
              valid: 'Incorrect'
            },
            {
              option: 'A free text field',
              valid: 'Correct'
            },
            {
              option: 'A picklist of predefined text options',
              valid: 'Correct'
            },
            {
              option: 'A free text field with default text',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following are potential reasons why Approved Email content would not be visible to a user in Veeva CRM Online/Mobile?',
          answers: [
            {
              option: 'The Approved Email documents have not been successfully synced to Veeva CRM',
              valid: 'Correct'
            },
            {
              option: 'The Approved Email documents are not set to the correct state in Veeva Vault PromoMats',
              valid: 'Correct'
            },
            {
              option: 'The Veeva CRM user is not aligned to the same product as the Approved Email documents',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'HCP actions or requests from an Approved Email they have received (e.g. opting in for an event or requesting an MSL visit) can be captured as Multichannel Activity records.',
          answers: [
            {
              option: 'False',
              valid: 'Inorrect'
            },
            {
              option: 'True',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Can email fragments be used to directly send email attachments?',
          answers: [
            {
              option: 'No',
              valid: 'Correct'
            },
            {
              option: 'True',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following statemtns regarding images in Approved Emails are true?',
          answers: [
            {
              option: 'Images uploaded as Assets under an Approved Email document will be published to the Veeva Content Delivery Network',
              valid: 'Correct'
            },
            {
              option: 'Images utilized within an Approved Email document should be uploaded as a zip under "Assets"',
              valid: 'Correct'
            },
            {
              option: 'Content creators need to manually update image paths to point to the new image locations once they are published to the Veeva Content Delivery Network',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following use cases can be supported by Approved Email? (select all that apply)',
          answers: [
            {
              option: 'Share content',
              valid: 'Correct'
            },
            {
              option: 'Announce product news',
              valid: 'Correct'
            },
            {
              option: 'Create pre-launch awareness',
              valid: 'Correct'
            },
            {
              option: 'Drive to web content',
              valid: 'Correct'
            },
            {
              option: 'Gather feedback',
              valid: 'Correct'
            },
            {
              option: 'Fulfill a medical inquiry',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'When sending hyperlinks via Approved Email, URLs can be tagged with attributes from which Veeva CRM Objects?',
          answers: [
            {
              option: 'Key Message',
              valid: 'Incorrect'
            },
            {
              option: 'User',
              valid: 'Correct'
            },
            {
              option: 'Call',
              valid: 'Incorrect'
            },
            {
              option: 'Account',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Custom Text tokens can be utilized to allow end users (e.g. reps) to manually enter values into the "From" and "Reply To" email header fields.',
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
          question: 'It is possible to insert Email Fragments in multiple places within one Email Template',
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
          question: 'Template Fragments are used as a framework to automatically generate Email Fragments',
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
          question: 'Where does a content administrator define the minimum and maximum number of Email Fragments that an end user can insert into an Email Template?',
          answers: [
            {
              option: 'In the document properties in Veeva Vault PromoMats',
              valid: 'Incorrect'
            },
            {
              option: 'In the Sent Email object in Veeva CRM Online',
              valid: 'Incorrect'
            },
            {
              option: 'Within the Token used in the Email Template HTML',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following can be embedded on a custom (customer-owned) landing page?',
          answers: [
            {
              option: 'Vault Viewer',
              valid: 'Correct'
            },
            {
              option: 'Unsubscribe Page',
              valid: 'Correct'
            },
            {
              option: 'Surveys',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which Configuration Token should be used to insert a Template Fragment into an Email Template?',
          answers: [
            {
              option: '##insertEmailFragments##',
              valid: 'Incorrect'
            },
            {
              option: '{{insertEmailFragments}}',
              valid: 'Incorrect'
            },
            {
              option: '{{emailTemplateFragment}}',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following area automatically tracked and recorded when an Approved Email is sent?',
          answers: [
            {
              option: 'Deliveries',
              valid: 'Correct'
            },
            {
              option: 'Opens',
              valid: 'Correct'
            },
            {
              option: 'Document views',
              valid: 'Correct'
            },
            {
              option: 'Clicks',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'It is possible to provide end users (e.g. reps) with a picklist of potential subject lines to choose from when they send an Approved Email.',
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
          question: 'When sending meeting invites via Approved Email, calendar invites (.ics files) can be attached to which type of event?',
          answers: [
            {
              option: 'Engage Meeting',
              valid: 'Correct'
            },
            {
              option: 'Events Management',
              valid: 'Correct'
            },
            {
              option: 'Medical Events',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'When launching Approved Email directly from a CLM Presentation, it is possible to specify both the Email Template to be opened and the Email Fragments to be inserted into it.',
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
          question: 'When using Approved Email to send a HCP a receipt of a transaction (e.g. requesting a product sample or raising a medical inquiry), it is possible to capture the HCPs signature in Veeva Mobile CRM and dynamically insert this into the email.',
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
          question: 'When a Survey is sent to a HCP via Approved Email, where does the HCP complete that survey?',
          answers: [
            {
              option: 'Directly in the Approved Email received in their inbox',
              valid: 'Incorrect'
            },
            {
              option: 'In their browser on a Veeva-hosted website, having clicked on a hyperlink in the Approved Email',
              valid: 'Correct'
            },
            {
              option: 'In their browser on a customer-hosted website, having clicked on a hyperlink in the Approved Email',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following would require using the Customer Content Configuration Token?',
          answers: [
            {
              option: 'Dynamically inserting the Account (HCP) name into an Email Template',
              valid: 'Incorrect'
            },
            {
              option: 'Dynamically inserting the User (rep) email address into an Email Template',
              valid: 'Incorrect'
            },
            {
              option: 'Dynamically inserting formulary information into an Email Template',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'From which of the follwoing Veeva CRM objects is it possible to tag URLs in Approved Emails with values? (select all that apply)?',
          answers: [
            {
              option: 'Account',
              valid: 'Correct'
            },
            {
              option: 'Call',
              valid: 'Incorrect'
            },
            {
              option: 'Key Message',
              valid: 'Incorrect'
            },
            {
              option: 'User',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'When using the {{$VaultDocumentID}} token, remember to pull this Documnet ID from:',
          answers: [
            {
              option: 'The Document\'s Vault URL',
              valid: 'Correct'
            },
            {
              option: 'The Document\'s CRM URL',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Additional pieces can be associated to the Email Fragment by adding them as "Other Documents" and using which of the following tokens?',
          answers: [
            {
              option: '"$VaultDocumentID"',
              valid: 'Incorrect'
            },
            {
              option: '{{$VaultDocumentID}}',
              valid: 'Correct'
            },
            {
              option: '($VaultDocumentID)',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Only one Material (Promotional Piece), ISI and PI can be assigned to an Email Fragment using {{PieceLink}}, {{ISILink}} and {{PILink}}, respectively',
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
          question: 'It is possible to link multiple Veeva Vault PromoMats documents to a single Email Fragment.',
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
          question: 'In order to record HCP clicks on links within an Approved Email in Veeva CRM, labels must be added to the hyperlinks.',
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
          question: 'HCP actions or requests from an Approved Email they have received (e.g. opting in for an event or requesting an MSL visit) can be captuired as Multichannel Activity records.',
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
          question: 'Content administrators can choose to define the exact Email Fragments available for end users to insert into each Email Template.',
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
          question: 'Dynamically inserted footnotes and citations can be previewed by the end user before sending an Approved Email.',
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
          question: 'Which of the following best describes how footnotes and citations can be inserted into Approved Emails?',
          answers: [
            {
              option: 'They are dynamically inserted into the Email Template based on the Email Fragments selected by the end user',
              valid: 'Correct'
            },
            {
              option: 'They are manually inserted into the Email Template by the end user',
              valid: 'Incorrect'
            },
            {
              option: 'They are dynamically inserted into the Email Fragments based on the Email Template selected by the end user',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following are potential reasons for Approved Email content not being visible to a User in Veeva CRM Online/Mobile? (select all that apply)',
          answers: [
            {
              option: 'The Approved Email documents are not set to the correct states in Veeva Vault PromoMats',
              valid: 'Correct'
            },
            {
              option: 'The Approved Email documents have not been successfully synced to Veeva CRM',
              valid: 'Correct'
            },
            {
              option: 'The Veeva CRM User is not aligned to the same product as the Approved Email documents',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Where is the "Approved Emails Test Email Address" set in Veeva CRM Online?',
          answers: [
            {
              option: 'Approved Email Administration tab',
              valid: 'Incorrect'
            },
            {
              option: 'Setup>>App Setup, Develop, Custom Settings>>Approved Email Settings (click: Edit)',
              valid: 'Incorrect'
            },
            {
              option: 'Setup>>App Setup, Develop, Custom Settings>>Approved Email Settings (click: Manage)',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Email Templates set to "Staged" state in Veeva Vault PromoMats will be visible to all Veeva CRM Users once synced.',
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
          question: 'Where can a Veeva CRM user view the status of an Approved Email they have sent?',
          answers: [
            {
              option: 'Approved Document record in Veeva CRM Online',
              valid: 'Incorrect'
            },
            {
              option: 'Sent Email record in Veeva CRM Online/Mobile',
              valid: 'Correct'
            },
            {
              option: 'Email Template document metadata in Veeva Vault PromoMats',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following will ensure that Veeva CRMs built-in consent management does not prevent a user from sending an Approved Email to an Account for testing?',
          answers: [
            {
              option: 'Set the "Approved Email Test Email Address" to the user\'s own email address',
              valid: 'Incorrect'
            },
            {
              option: 'Ensure that the "Approved Email Admin" checkbox is ticked on the user record',
              valid: 'Incorrect'
            },
            {
              option: 'Set the "Approved Email Consent" field to "Implicit Opt In" or create an opt in (Multichannel Consent) record for that account',
              validL: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following are potential Approved Email entry points in Veeva Mobile CRM? (select all that apply)',
          answers: [
            {
              option: 'Account Page (Account Detail)',
              valid: 'Correct'
            },
            {
              option: 'Call Report',
              valid: 'Correct'
            },
            {
              option: 'CLM Presentation',
              valid: 'Correct'
            },
            {
              option: 'Documents',
              valid: 'Incorrect'
            },
            {
              option: 'Account List (My Accounts)',
              valid: 'Correct'
            },
            {
              option: 'My Schedule',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following email header values cannot be defined for an Email Template within Veeva Vault PromoMats?',
          answers: [
            {
              option: 'Cc',
              valid: 'Correct'
            },
            {
              option: 'Reply To Address',
              valid: 'Incorrect'
            },
            {
              option: 'Subject',
              valid: 'Incorrect'
            },
            {
              option: 'Bcc',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Promotional Pieces and Reference Documents must be set to the "Approved" state in Veeva Vault PromoMats if linked to from an Email Template or Email Fragment?',
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
          question: 'Bcc recipients can be defined by content administrators or by end users (e.g. reps) depending on configuration.',
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
          question: 'The email header "Subject" field can be hard coded or utilize Custom Text or Merge Tokens to enable personalization.',
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
          question: 'Where should email header information (from address, subject, etc) be defined for Email Templates?',
          answers: [
            {
              option: 'In the Email Template HTML file',
              valid: 'Incorrect'
            },
            {
              option: 'In Veeva CRM Online',
              valid: 'Incorrect'
            },
            {
              option: 'In the Email Template document metadata in Veeva Vault PromoMats',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following statements about the BEE Editor are true? (select all that apply)',
          answers: [
            {
              option: 'No knowledge of HTML is required to use the BEE Editor',
              valid: 'Correct'
            },
            {
              option: 'The BEE Editor can be used to create Email Templates and Email Fragments',
              valid: 'Incorrect'
            },
            {
              option: 'Only Email Templates originally created using the BEE Editor ca be edited using it',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'What is the correct format of the expanded markup syntax Merge Token used to dynamically pull values from the Account, User and Approved Document objects?',
          answers: [
            {
              option: '{{ObjectAPIName_FieldAPIName}}',
              valid: 'Incorrect'
            },
            {
              option: '{{ObjectAPIName.FieldAPIName}}',
              valid: 'Correct'
            },
            {
              option: '{{ObjectLabel.FieldLabel}}',
              valid: 'Incorrect'
            },
            {
              option: '##ObjectAPIName.FieldAPIName##',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Configuration Tokens are only supported in Email Fragments if they are used within href tags and require no User input.',
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
          question: 'Which characters should surround Merge Tokens when they are used within a Custom Text token?',
          answers: [
            {
              option: '{{MergeToken}}',
              valid: 'Incorrect'
            },
            {
              option: '((MergeToken))',
              valid: 'Incorrect'
            },
            {
              option: '[[MergeToken]]',
              valid: 'Incorrect'
            },
            {
              option: '##MergeToken##',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Custom Text Tokens must include default text',
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
          question: 'Using Merge Tokens, dynamic values can be pulled into an Email Template from which of the following objects? (select all that apply)',
          answers: [
            {
              option: 'Account',
              valid: 'Correct'
            },
            {
              option: 'Approved Document',
              valid: 'Correct'
            },
            {
              option: 'Key Message',
              valid: 'Incorrect'
            },
            {
              option: 'User',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Email Fragment content must be encapsulated in a &lt;tr&gt; &lt;/tr&gt; tag.',
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
          question: 'When considering Approved Email content creation best practices, which of the following statements are true? (select all that apply)',
          answers: [
            {
              option: 'Ensure that the content looks like a marketing email',
              valid: 'Incorrect'
            },
            {
              option: 'Ensure content is relevant and regularly refreshed',
              valid: 'Correct'
            },
            {
              option: 'Personalized content using Configuration Tokens',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Excluding the BEE Editor, what can content creators use to generate the HTML required for Approved Email Templates?',
          answers: [
            {
              option: 'Veeva CRM Online',
              valid: 'Incorrect'
            },
            {
              option: 'Veeva Vault PromoMats',
              valid: 'Incorrect'
            },
            {
              option: 'Any HTML editor/authoring tool',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following statements about Apporved Email consent management are true? (select all that apply)',
          answers: [
            {
              option: 'Veeva CRM has built-in consent management for Approved Email',
              valid: 'Correct'
            },
            {
              option: 'Veeva provides a configurable, pre-hosted unsubscribe page',
              valid: 'Correct'
            },
            {
              option: 'It is possible for customers to embed the unsubscribe page on another website',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following statements regarding Vault Viewer are correct? (select all that apply)',
          answers: [
            {
              option: 'It can be used by the recipient to view the received Approved Email in their browser',
              valid: 'Incorrect'
            },
            {
              option: 'It can be standalone (no configuration required) or embedded on an external webpage',
              valid: 'Correct'
            },
            {
              option: 'It can be configured to allow recipients to download Reference Documents and Promotional Pieces',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which of the following statements about Vault Viewer are true? (select all that apply)',
          answers: [
            {
              option: 'Documents can be made available for the email recipient to download via the Vault Viewer',
              valid: 'Correct'
            },
            {
              option: 'The customer must host the Vault Viewer on their own website',
              valid: 'Incorrect'
            },
            {
              option: 'If a document is withdrawn in Veeva Vault PromoMats then the email recipient will no longer be able to view it in the Vault Viewer',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'How are Reference Documents and Promotional Pieces shared with Approved Email recipients?',
          answers: [
            {
              option: 'They are attached to the email',
              valid: 'Incorrect'
            },
            {
              option: 'The email includes links to view the documents in the Vault Viewer',
              valid: 'Correct'
            },
            {
              option: 'Hard copies are mailed separately',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following is used to automatically generate an Email Fragment from any document in Veeva Vault PromoMats?',
          answers: [
            {
              option: 'Email Template',
              valid: 'Incorrect'
            },
            {
              option: 'Template Fragment',
              valid: 'Incorrect'
            },
            {
              option: 'Master Email Fragment',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'Which document type is the core component of an Approved Email?',
          answers: [
            {
              option: 'Master Email Fragment',
              valid: 'Incorrect'
            },
            {
              option: 'Email Fragment',
              valid: 'Incorrect'
            },
            {
              option: 'Email Template',
              valid: 'Correct'
            },
            {
              option: 'Template Fragment',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Where are Approved Email reports (e.g. a "Sent Email by Account" report) usually created and viewed?',
          answers: [
            {
              option: 'Veeva Vault PromoMats',
              valid: 'Incorrect'
            },
            {
              option: 'Veeva CRM Online',
              valid: 'Correct'
            },
            {
              option: 'Veeva Mobile CRM',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Approved Email Templates can be uploaded directly to Veeva CRM Online if the customer does not have Veeva Vault PromoMats.',
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
          question: 'Where do administrators upload Approved Email content?',
          answers: [
            {
              option: 'Veeva Vault PromoMats',
              valid: 'Correct'
            },
            {
              option: 'Veeva CRM Online',
              valid: 'Incorrect'
            },
            {
              option: 'Veeva Multichannel Engine',
              valid: 'Incorrect'
            }
          ]
        },
        {
          question: 'Which of the following use cases can be supported by Approved Email? (select all that apply)',
          answers: [
            {
              option: 'Arrange or confirm a meetings',
              valid: 'Correct'
            },
            {
              option: 'Follow up after a meeting or a no-show',
              valid: 'Correct'
            },
            {
              option: 'Send an event invite',
              valid: 'Correct'
            },
            {
              option: 'Share content',
              valid: 'Correct'
            },
            {
              option: 'Announce product news',
              valid: 'Correct'
            },
            {
              option: 'Create pre-launch awareness',
              valid: 'Correct'
            }
          ]
        },
        {
          question: 'End users can send Approved Emails from which of the following? (select all that apply)',
          answers: [
            {
              option: 'Veeva CRM Online',
              valid: 'Correct'
            },
            {
              option: 'Veeva Mobile Online',
              valid: 'Correct'
            },
            {
              option: 'Veeva Vault PromoMats',
              valid: 'Incorrect'
            }
          ]
        }
      ]
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
      return this.vae
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
