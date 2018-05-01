# Intro
- components shouldn't be an add-on complexity layer & it should be kept as dump as possible.

- this way its easier to maintain the app because you can add any extra inputs you want & add the validation logic to the backend without ever touching the components files.

# Installation

```bash
npm install vue axios vue-notif --save
```

# Usage
**1-** first register the components

- we use ***Bulma*** for styling.

```js
window.Vue = require('vue')
window.axios = require('axios')
window.EventHub = require('vuemit')

// For Laravel
window.axios.defaults.headers.common = {
    'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').getAttribute('content'),
    'X-Requested-With': 'XMLHttpRequest'
};

// Shared Storage
window.StorageHub = new Vue({
    data: {
        formData: {}
    }
})

// Components
Vue.component('MyForm', require('./path/to/Form.vue'))
Vue.component('FormInput', require('./path/to/Input.vue'))
Vue.component('MyNotification', require('vue-notif'))
```

**2-** make sure your backend return errors payload as an `array`.

## Example
- MyForm
    ```html
    <my-form inline-template>

        <form action="url"
              method="post"
              @submit.prevent="FormSubmit($event)">

            <!-- form inputs -->
            ...

            <!-- submit -->
            <button type="submit"
                    :disabled="isSubmitting"
                    :class="{'is-loading': isSubmitting}">
                    Submit
            </button>
        </form>

    </my-form>
    ```

- FormInput
    ```html
    // for hidden inputes
    <form-input inline-template>
        <input type="hidden" name="token" value="abc">
    </form-input>

    // for normal inputs
    <form-input inline-template :get-errors="errors.email">
        <div>
            <label for="email">E-Mail Address</label>
            <input type="email"
                   name="email"
                   v-model="input"
                   @blur="getName($event)"
                   :class="classObject">
        </div>
    </form-input>

    // for radio/checkbox
    <form-input inline-template :get-errors="errors.email">
        <div>
            <label>
                <input type="checkbox"
                       name="remember"
                       v-model="input"
                       @click="getName($event)">
                       Remember me
            </label>
        </div>
    </form-input>
    ```
> :get-errors="errors.the-input-name"

- FormErrors
    ```html
    <form-input>
        // ...
        <form-errors :errors="showErrors"></form-errors>
    </form-input>
    ```

