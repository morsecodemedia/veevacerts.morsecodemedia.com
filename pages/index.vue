<template>
  <div class="homepage">
    <h1>
      Veeva Certs
    </h1>
    <p>A tool for studying for Veeva certifications.</p>
    <div
      v-if="(tests.length > 0)"
      class="link-container"
    >
      <nuxt-link
        v-for="t in tests"
        :key="t.data"
        :to="t.url"
      >
        {{ t.label }}
      </nuxt-link>
    </div>
    <div
      v-else
      class="link-container"
    >
      <p>There currently aren't any study exams available at this time.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data () {
    return {
      tests: [
        {
          data: 'clmTechV2',
          label: 'CLM Technical Certification v2',
          url: '/clm-technical-v2/'
        },
        {
          data: 'vaeTechV2',
          label: 'Approved Email Technical Certification v2',
          url: '/vae-technical-v2/'
        },
        {
          data: 'engageTechV2',
          label: 'Engage Meeting Technical Certification v2',
          url: '/engage-technical-v2/'
        },
        {
          data: 'promomatsReviewApprovalV2',
          label: 'PromoMats Reivew & Approval v2',
          url: '/promomats-review-and-approval-v2/'
        }
      ]
    }
  },
  head () {
    return {
      title: 'Veeva Certs | A morsecodemedia tool',
      meta: [
        { hid: 'ogtitle', property: 'og:title', content: 'Veeva Certs | A morsecodemedia tool' },
        { hid: 'twtitle', name: 'twitter:title', content: 'Veeva Certs | A morsecodemedia tool' },
        { hid: 'googlename', itemprop: 'name', content: 'Veeva Certs | A morsecodemedia tool' },
        { hid: 'description', name: 'description', content: 'A tool for studying for Veeva certifications.' },
        { hid: 'ogdescription', property: 'og:description', content: 'A tool for studying for Veeva certifications.' },
        { hid: 'twdescription', name: 'twitter:description', content: 'A tool for studying for Veeva certifications.' },
        { hid: 'googledescription', itemprop: 'description', content: 'A tool for studying for Veeva certifications.' },
        { hid: 'ogurl', property: 'og:url', content: 'https://veevacerts.morsecodemedia.com' + this.$route.path },
        { hid: 'twsite', name: 'twitter:site', content: 'https://veevacerts.morsecodemedia.com' + this.$route.path }
      ],
      link: [
        { hid: 'canonical', rel: 'canonical', href: 'https://veevacerts.morsecodemedia.com' + this.$route.path }
      ]
    }
  }
}
</script>

<style lang="scss">
.homepage {
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
.link-container {
  display: flex;
  flex-direction: column;
}
</style>
