<template lang="pug">
    div
        label.typo__label Customized multiselect
        multiselect(
        placeholder="Pick at least one"
        v-model="value"
        :options="options"
        :searchable="true"
        :max-height="150"
        @no-result="onNoResult"
        :clickable-no-results="true"
        label="nombre"
        track-by="id"
        :show-labels="false"
        :highlightSelectedOption="false"
        :preserve-search="true"
        )
            template(slot="clear", slot-scope="props")
              div.multiselect__clear(
                v-if="value",
                @mousedown.prevent.stop="clear()"
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
      value: null,
      options: [
        {
          id: 1,
          nombre: 'a'
        },
        {
          id: 2,
          nombre: 'b'
        }
      ]
    }
  },
  methods: {
    onNoResult (search) {
      window.alert('Abriendo ventana modal para crear un nuevo registro ' + search)
    },
    clear () {
      this.value = null
    }
  }
}
</script>

<style lang="scss" scoped>
	.form__label {
		margin-top: 5px !important;
	}
  .multiselect__clear {
    position: absolute;
    right: 41px;
    height: 40px;
    width: 40px;
    display: block;
    cursor: pointer;
    z-index: 3;
  
    &:before, &:after {
      content: "";
      display: block;
      position: absolute;
      width: 3px;
      height: 16px;
      background: #aaa;
      top: 12px;
      right: 4px;
    }
  
    &:before {
      transform: rotate(45deg)
    }
  
    &:after {
      transform: rotate(-45deg)
    }
  }
</style>
