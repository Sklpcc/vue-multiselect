<template lang="pug">
    div
        label.typo__label Customized multiselect
        multiselect(
        placeholder="Pick at least one",
        :value="value",
        :options="options",
        :searchable="true",
        :max-height="150",
        @input="onChange",
        @search-change="onSearchChange",
        :loading="loading",
        @no-result="onNoResult",
        :clickable-no-results="false"
        )
            template(slot="noResult", slot-scope="props") Crear {{ props.search }}...
</template>

<script>
import Multiselect from 'vue-multiselect'
import axios from 'axios'

export default {
  components: {
    Multiselect
  },
  data () {
    return {
      isTouched: false,
      value: '',
      options: ['anastasio', 'benito', 'caceres', 'dedalo', 'deuteronomio', 'dedo', 'datil', 'docil', 'dedicado'],
      loading: false
    }
  },
  methods: {
    onChange (value) {
      this.value = value
    },
    onSearchChange (searchQuery, id) {
      console.log(searchQuery)
      this.loading = true
      axios.get('http://localhost:3001/test/' + searchQuery)
        .then(response => {
// eslint-disable-next-line no-undef
          this.options = response.data
        })
        .catch(reason => {
          console.error(reason)
        })
        .finally(() => {
          this.loading = false
        })
    },
    onNoResult (search) {
      window.alert('Abriendo ventana modal para crear un nuevo registro ' + search)
    }
  }
}
</script>

<style lang="css">
	.form__label {
		margin-top: 5px !important;
	}
</style>
