<template>
  <div>
    <div id="skip">
      <a class="skip-main" href="#main">Skip to main content</a>
    </div>
    <nuxt
      id="main"
      ref="main"
      aria-label="main"
      role="main"
    />
  </div>
</template>

<script>

let bodyTag = null

export default {
  name: 'App',
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
        { hid: 'ogurl', property: 'og:url', content: 'https://veevacerts.morsecodemedia.com/' + this.$route.path },
        { hid: 'twsite', name: 'twitter:site', content: 'https://veevacerts.morsecodemedia.com/' + this.$route.path }
      ],
      link: [
        { hid: 'canonical', rel: 'canonical', href: 'https://veevacerts.morsecodemedia.com/' + this.$route.path }
      ],
      bodyAttrs: {
        class: 'page-' + ((this.$route.path.length > 1) ? this.$route.path.slice(1).replace(/\/$/, '').replace(/\//g, '-') : 'home')
      }
    }
  },
  mounted () {
    bodyTag = document.getElementsByTagName('body')[0]
    bodyTag.classList.remove('killscroll')
  }
}
</script>
