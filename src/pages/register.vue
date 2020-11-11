<template>
<div class="signup">
    <h2>Create account</h2>
  <v-form>
    <v-container>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="title"
            :rules="[rules.required, rules.counter]"
            label="Title"
            counter
            maxlength="20"
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="email"
            :rules="[rules.required, rules.email]"
            label="E-mail"
          ></v-text-field>
          <v-text-field
      v-model="value"
      color="cyan darken"
      label="Text field"
      placeholder="Start typing..."
      loading
    >
      <template v-slot:passwordStrength>
        <v-progress-linear
          v-if="custom"
          :value="passwordStrength"
          :color="color"
          absolute
          height="7"
        ></v-progress-linear>
      </template>
    </v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</div>
</template>

<script>
export default {
  name: 'Register',
    components:{

    },
    data () {
      return {
        title: 'Preliminary report',
        email: '',
        rules: {
          required: value => !!value || 'Required.',
          counter: value => value.length <= 20 || 'Max 20 characters',
          email: value => {
            const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
            return pattern.test(value) || 'Invalid e-mail.'
          },
        },
      }
    },

    computed: {
      passwordStrength () {
        return Math.min(100, this.value.length * 10)
      },
      color () {
        return ['error', 'warning', 'success'][Math.floor(this.passwordStrength / 40)]
      }
    }
}
</script>