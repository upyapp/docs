<i>Last updated: August 2, 2022 9:59 AM</i>

### Form validation guide
This is a guide of how to use form validation on our [web-next](https://github.com/uuppyy/web-next) app, the validation using `useValidator` composable function, you can learn how it works [here](https://github.com/uuppyy/web-next/blob/main/composables/useValidator.ts).

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

#### Rules available
| Rule          | Description                                                         |
--------------- | ------------------------------------------------------------------- |
| required      | The field cannot be empty and must be filled                        |
| email         | The field must contain a string of email format                     |
| min:[number]  | The field must contain a string that have at least X characters     |
| max:[number]  | The field must contain a string that have at max X characters       |
| containSymbol | The field must contain a string that mixed with symbol character    |
| containNumber | The field must contain a string that mixed with number              |
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
