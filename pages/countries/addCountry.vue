<template>
<div class="d-flex justify-center">
  <form>
    <v-text-field
      v-model="name"
      :error-messages="nameErrors"
      :counter="20"
      label="Country name"
      required
      @input="$v.name.$touch()"
    ></v-text-field>
    <v-text-field
    v-model="numberValue"
    hide-details
    label="Population"
    single-line
    
    />
    <v-select class="mt-5"
      v-model="select"
      :items="items"
      :error-messages="selectErrors"
      label="Continent"
      required
      @change="$v.select.$touch()"
    ></v-select>
    <v-text-field
      v-model="url"
      label="Picture url"
      required
    ></v-text-field>
    <v-textarea
        v-model="textarea"
        name="textarea"
        label="Description"
        hint="Hint text"
    ></v-textarea>
    <v-btn
      class="mr-4"
      @click="submit"
    >
      submit
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
  </form>
</div>
</template>
<script>
  import { validationMixin } from 'vuelidate'
  import { required, maxLength } from 'vuelidate/lib/validators'

  export default {
    mixins: [validationMixin],

    validations: {
      name: { required, maxLength: maxLength(20) },
      number: { required, maxLength: maxLength(10) },
      select: { required },
    },

    data: () => ({
      name: '',
      numberValue: null,
      select: null,
      items: [
        'Europe',
        'Asia',
        'America',
        'Africa',
        'Oceania',
      ],
      url: '',
      textarea: ''
    }),

    computed: {
         
      selectErrors () {
        const errors = []
        if (!this.$v.select.$dirty) return errors
        !this.$v.select.required && errors.push('Continent is required')
        return errors
      },
      nameErrors () {
        const errors = []
        if (!this.$v.name.$dirty) return errors
        !this.$v.name.maxLength && errors.push('Country name must be at most 20 characters long')
        !this.$v.name.required && errors.push('Name is required.')
        return errors
      },
    },

    methods: {
      submit () {
        this.$v.$touch()
        addCountry;
      },
      clear () {
        this.$v.$reset()
        this.name = ''
        this.select = null
        this.numberValue = null
        this.url = ''
        this.textarea = ''
      },
    },
  }
</script>