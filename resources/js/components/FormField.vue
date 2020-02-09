<template>
  <default-field
    :field="field"
    :errors="errors"
  >
    <template slot="field">
      <span v-text="value" />
      <input
        :id="field.name"
        v-model="value"
        :class="errorClasses"
        class="w-full form-control form-input shadow-none"
        type="range"
        min="-50"
        max="50"
      >
    </template>
  </default-field>
</template>

<script>
import { FormField, HandlesValidationErrors } from 'laravel-nova'

export default {
    mixins: [FormField, HandlesValidationErrors],

    props: ['resourceName', 'resourceId', 'field'],

    methods: {
        /*
         * Set the initial, internal value for the field.
         */
        setInitialValue() {
            this.value = this.field.value || 0
        },

        /**
         * Fill the given FormData object with the field's internal value.
         */
        fill(formData) {
            formData.append(this.field.attribute, this.value || 0)
        },

        /**
         * Update the field's internal value.
         */
        handleChange(value) {
            this.value = value
        },
    },
}
</script>
