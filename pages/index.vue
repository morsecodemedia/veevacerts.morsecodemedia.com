<template>
  <div class="homepage">
    <h1>
      Veeva Certs
    </h1>
    <p>A tool for studying for Veeva certifications.</p>
    <div class="link-container">
      <nuxt-link to="/clm-technical-v2/">
        CLM Technical Certification v2
      </nuxt-link>
      <nuxt-link to="/vae-technical-v2/">
        Approved Email Technical Certification v2
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data () {
    return {
      disabled: true
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
