# Requirement

[Axios](https://github.com/mzabriskie/axios)

[Notification Component](https://github.com/ctf0/Notification-Component)

# Intro
- when using with something like laravel, components shouldnt be an add-on complexity layer, instead it should be kept as dump as possible.

- its easier to maintain the app because you can add any extra inputs you want & add the validation logic to the backend without ever touching the components files.

# Usage
**1-** first register the components

- we use ***Bulma*** for styling, but you can change it by editing the components files.

```js
window.axios = require('axios')
window.Vue = require('vue')

// Axios + Laravel
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
Vue.component('FormErrors', require('./path/to/Errors.vue'))
```

**2-** make sure your backend return errors payload as an `array`.

## Example
- MyForm
    ```html
    <my-form inline-template>

        <form action="url"
              method="post"
              class="column"
              @submit.prevent="FormSubmit($event)">

            <!-- form inputs -->
            ...

            <!-- submit -->
            <div class="field">
                <div class="control">
                    <button type="submit"
                            class="button is-info"
                            :disabled="isSubmit"
                            :class="{'is-loading': isSubmit}">
                        Submit
                    </button>
                </div>
            </div>
        </form>

    </my-form>
    ```

- FormInput
    ```html
    // for pre-defeined values
    <form-input inline-template>
        <input type="hidden" name="token" value="abc">
    </form-input>

    // for normal inputs
    // :get-errors="errors.inputName"
    <form-input inline-template :get-errors="errors.email">
        <div class="field">
            <label for="email" class="label">E-Mail Address</label>
            <div class="control">
                <input type="email"
                       name="email"
                       class="input"
                       v-model="input"
                       @input="getName($event)"
                       :class="classObject">
            </div>
        </div>
    </form-input>
    ```

- FormErrors
    ```html
    <form-input>
        // ...
        <form-errors :errors="showErrors"></form-errors>
    </form-input>
    ```

# ToDo
* [ ] add support to **`input type="file"`**.
* [ ] Turn into Package.
