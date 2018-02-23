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
        :clickable-no-results="true",
        :internal-search="false"
        )
            template(slot="noResult", slot-scope="props") Crear {{ props.search }}...
</template>

<script>
import Multiselect from 'vue-multiselect'

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
      new Promise(resolve => {
        setTimeout(resolve, 200)
      })
      .then(response => {
        this.options = ['dedalo', 'deuteronomio', 'dedo', 'datil', 'docil', 'dedicado']
        .filter(item => {
          return item.startsWith(searchQuery)
        })
        this.loading = false;
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
