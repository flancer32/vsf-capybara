<template>
  <div>
    <a href="#" @click.prevent="showLanguagesModal">
      {{ linkName }}
    </a>
    <modal-switcher v-if="loadLanguagesModal" />
  </div>
</template>

<script>
import config from 'config';
import { currentStoreView } from '@vue-storefront/core/lib/multistore';
const ModalSwitcher = () =>
  import(
    /* webpackChunkName: "vsf-modals" */ 'theme/components/core/blocks/Switcher/Language'
  );

export default {
  components: {
    ModalSwitcher
  },
  data () {
    return {
      loadLanguagesModal: false
    };
  },
  computed: {
    linkName () {
      const { i18n = config.i18n } = currentStoreView();
      return `${i18n.defaultCountry} / ${i18n.defaultLanguage} / ${i18n.currencyCode}`;
    }
  },
  methods: {
    showLanguagesModal () {
      this.loadLanguagesModal = true;
      this.$bus.$emit('modal-show', 'modal-switcher');
    }
  }
};
</script>
