<i>Last updated: August 1, 2022 5:40 PM</i>

### Form validation guide
This is guide on how to use form validation on our [web-next](https://github.com/uuppyy/web-next) app, the validation using `useValidator` composable functions, you can learn how it works [here](https://github.com/uuppyy/web-next/blob/main/composables/useValidator.ts).

#### Tag used
```
<n-validate>
  <input
    ...
    rules="rule_1|rule_2|rule_3|rule_4:value"
  >
</n-validate>
```

#### `<n-validate>` tag props
| Attr  | Format | Description                                                                        |
------- | ------ | ------------------------------------------------------------------------------------
| for   | string | must be the same as input v-model ref                                              |
| :name | string | input name, this will be used for error message, you can pass localization here    |

#### `<input>` tag props
| Attr  | Format                           | Description            |
------- | -------------------------------- | ---------------------- |
| rules | string separated by pipe symbol  | collection of rules    |
<br>

#### Full Usage Example
```
<template>
  <form id="login" @submit.prevent="login('login')">
    <!-- input: email or username -->
    <n-validate 
      for="emailUsername" 
      :name="$t('logins.form.email_username')"
    >
      <input 
        v-model="inputs.emailUsername"
        type="text"
        rules="required|email"
        :placeholder="$t('logins.form.email_username')"
      >
    </n-validate>

    <!-- input: password -->
    <n-validate 
      for="password" 
      :name="$t('logins.form.password')"
    >
      <input
        v-model="inputs.password"
        type="password"
        autocomplete="off"
        rules="required|min:6|max:16"
        :placeholder="$t('logins.form.password')"
      >
    </n-validate>

    <button type="submit">LOGIN</button>
  </form>
</template>

<script setup>
import { useI18n } from 'vue-i18n'
const { t } = useI18n()

const inputs = ref({
  emailUsername: '',
  password: ''
})

const login = () => {
  validate()
}

const validate = () => {
  const loginEl = document.getElementById('login')
  useValidator().validate(loginEl, t) // composable 'useValidator()', auto-imported in Nuxt3
}
</script>
```
